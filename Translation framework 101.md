# Table of Contents
=================

* [Translation Framework](#translation-framework)
   * [OpenConfig to device config mapping](#openconfig-to-device-config-mapping)
     * [Finding mapping between device and the model](#finding-mapping-between-device-and-the-model)
     * [Documentation](#documentation)
   * [Translation Units in general](#translation-units-in-general)
     * [Module structure](#module-structure)
     * [Handlers](#handlers1)
   * [CLI Translation Unit](#cli-translation-unit)
      * [Readers](#readers1)
        * [Mandatory interfaces to implement](#mandatory-interfaces-to-implement1)
        * [Typed interfaces to implement (optional)](#typed-interfaces-to-implement-optional1)
        * [Util classes](#util-classes)
        * [Plaintext parsing hints](#plaintext-parsing-hints)
      * [Writers](#writers1)
        * [Mandatory interfaces to implement](#mandatory-interfaces-to-implement2)
        * [Existing noop writers](#existing-noop-writers1)
      * [TranslateUnit](#translateunit1)
   * [CLI Init Translation Unit](#cli-init-translation-unit)
   * [NETCONF Unified Translation Unit](#netconf-unified-translation-unit)
      * [Readers](#readers2)
        * [Mandatory interfaces to implement](#mandatory-interfaces-to-implement3)
        * [Typed interfaces to implement (optional)](#typed-interfaces-to-implement-optional2)
      * [Writers](#writers2)
        * [Mandatory interfaces to implement](#mandatory-interfaces-to-implement4)
        * [Existing noop writers](#existing-noop-writers2)
      * [TranslateUnit](#translateunit2)
   * [Translation units for different device versions](#translation-units-for-different-device-versions)
      * [Device registration](#device-registration)
      * [Handlers](#handlers2)
   * [Best practices for handlers (readers/writers)](#best-practices-for-handlers)

# <a name="translation-framework"></a>Translation Framework

The translation framework allows translation units to:

*   Add YANG model into the system
*   Register Handlers for all or a subset of nodes defined in the YANG model
*   Register the entire unit into the system, which is then able to perform


# <a name="openconfig-to-device-config-mapping"></a>OpenConfig to device config mapping


## <a name="finding-mapping-between-device-and-the-model"></a>Finding mapping between device and the model


Prefered YANG models for device config and operational data are [OpenConfig models](https://github.com/openconfig/public/tree/master/release/models).

These models usually represents configuration part in _container config_ and operational part in _container state_. Operational data is config data + operational data.

This site [http://ops.openconfig.net/branches/master/](http://ops.openconfig.net/branches/master/) may be used for better browsing in OpenConfig YANG models. Another option is to generate YANG tree representation by using _generate_html.sh_ in [https://github.com/FRINXio/openconfig](https://github.com/FRINXio/openconfig).

YANG models used in UniConfig framework need to be located in [https://github.com/FRINXio/openconfig](https://github.com/FRINXio/openconfig). In case the desired functionality is not modeled yet, you can create new YANG with its own structure or it can augment existing OpenConfig models. Guideline, how to write OpenConfig models can be found at [http://www.openconfig.net/docs/style-guide/](http://www.openconfig.net/docs/style-guide/).


## <a name="documentation"></a>Documentation

There is [translation-units-docs page](https://github.com/FRINXio/translation-units-docs) as a single point of truth for mapping.
**Use _{{ip}}_ notation** for variables in the templates. This notation is postman compatible.


# <a name="translation-units-in-general"></a>Translation Units in general


## <a name="module-structure"></a>Module structure

Translation unit is a self contained project which implements a mapping between OpenConfig based YANG models and device specific configuration. It is used by the FRINX ODL to perform translation between device specific configuration model and standard (OpenConfig) models. A unit usually consists of:



*   Handlers
    *   Readers
    *   Writers
*   TranslateUnit implementation
*   RPCs


## <a name="handlers1"></a>Handlers



*   Each complex node in YANG (container, list, augment...) should have a dedicated handler (Reader, Writer)
    *   This enables extensibility, readability and the framework can easily filter and process the data this way
    *   Unless there is a need to also handle child nodes, in which case register the handler using _subtreeAdd_ method from the registries
*   There are 2 types of handlers: Readers (Read operation) and Writers (Create, Update, Delete operation)
    *   One can implement just the readers or both readers and writers for YANG models. Writers must have counterpart readers because of reconciliation.
*   Readers and Writers should use the _InstanceIdentifier_ parameter they receive in _readCurrentAttributes_ or _writeCurrentAttributes_ methods to find information about keys for their parent nodes. E.g. Reader registered under ID: /interfaces/interface/config will always receive keyed version of that ID: /interface/interface[Loopback0]/config. So it can use method _firstKeyOf_ on _InstanceIdentifier_ to get the keys.
*   _RWUtils_ class contains methods for _InstanceIdentifier_ manipulation.
*   Readers and writers can be easily tested and it is necessary to provide unit tests for all of them. It's important to cover _readCurrentAttributes_ and _writeCurrentAttributes_ with all possible scenarios (all data there, no data there, partial data there...)
*   Writers may use **Preconditions.checkArgument()** before accessing the device. Fail of the precondition check does not invoke default rollback (opposite operation) on the writer where precondition is located.


# <a name="cli-translation-unit"></a>CLI Translation Unit

CLI Translation units are located in [https://github.com/FRINXio/cli-units](https://github.com/FRINXio/cli-units) repository. JAVA is used in CLI translation units.


### <a name="readers1"></a>Readers



*   Readers are handlers responsible for reading and parsing the data coming from a device
*   There are 2 types of readers: Reader and ListReader. Reader can be used to handle container or augmentation nodes and ListReader should handle list nodes from YANG.
    *   Both types need to implement **_readCurrentAttributes_** to fill the builder with appropriate values
    *   ListReader needs to also implement **_getAllIds()_** where it retrieves a key for each item to be present in current list. After the list is received, framework will invoke **_readCurrentAttributes_** for each item from getAllIds
*   Readers also need to implement boilerplate methods: 
    *   **_merge_**- cast the builder parameter to appropriate parent builder type e.g. in builder for /interfaces/interface you would perform: 
	
```
	((InterfacesBuilder)builder).setInterface(readValue)
```


*   Readers should always use overloaded **_blockingRead_** method which takes in the ReadContext since that method performs caching internally
*   **Use full version of commands** e.g. _show running-config interface_ instead of _sh run int_


#### <a name="mandatory-interfaces-to-implement1"></a>Mandatory interfaces to implement

Each reader needs to implement one of these interfaces based on type of target node in YANG. These interfaces also contain util methods which may be used for better manipulation with data. For more information about methods please read javadocs.

**CliConfigListReader** - implement this interface if target composite node in YANG is list and represents config data.

**CliConfigReader** - implement this interface if target composite node in YANG is container or augmentation and represents config data.

**CliOperListReader** - implement this interface if target composite node in YANG is list and represents operational data.

**CliOperReader** - implement this interface if target composite node in YANG is container or augmentation and represents operational data.

In cases where you want to invoke multiple readers on reading one YANG node, extend following abstract classes:

**CompositeListReader** - extend this abstract class if multiple list readers need to be invoked when reading specific list in YANG.

**CompositeReader** - extend this abstract class if multiple readers need to be invoked when reading specific node in YANG.

A practical example of their usage is reading network instance based on it's type. All child readers need to implement a check when the particular reader should be invoked or the parent reader should move on to the next reader.


#### <a name="typed-interfaces-to-implement-optional1"></a>Typed interfaces to implement (optional)

Interfaces which you may want to implement when some parent node in instance-identifier needs be checked for particular value or other data from data tree needs to be checked.

If data did not pass check, then reader implementing the interface will not be invoked by framework. Each descended reader needs to implement the interface as well.

**TypedListReader** - use when target composite node in YANG is list

**TypedReader** - use when target composite node in YANG is container or augmentation

For example typed readers for bgp (located under _protocol_) needs to check if _identifier_ in _protocol_ has value _BGP_. Otherwise readers for bgp will be invoked even if _protocol identifier_ is _OSPF_.


#### <a name="util-classes"></a>Util classes

**ParsingUtils** - use methods of this util class if you want to parse plaintext to java object builder


#### <a name="plaintext-parsing-hints"></a>Plaintext parsing hints

*   **Use** as **specific regular expressions** when parsing CLI output as possible
*   **For Cisco CLI devices** avoid using _section_ and other advanced formatting parameters. **Only | _include_ | _exclude_ and | _begin_ are allowed**.
*   Use CONFIG data as the source of truth when parsing information from device. Except when parsing state containers (or containers explicitly marked as _config false_).
    *   I.e. use _sh run_ | _include router ospf_ instead of _sh ospf_ when retrieving ospf routers list. 
    *   In some cases, it is not possible to just use config data e.g. _sh run interface_ does not show any data for interfaces that have no configuration. In this case it is necessary to use operational information from e.g. _sh ip int brief_
*   **Use following pattern when parsing multiline output from CLI**, where it is difficult to extract lines and their relationships
    *   I.e. when parsing configured BGP neighbors per address family following command can be used: **sh run | include ^router bgp|^ **address-family|^ *neighbor*** which results in:
	```
	router bgp 65000
     address-family ipv4 vrf vrf1
      neighbor 1.2.3.4 remote-as 65000>
	  neighbor 1.2.3.4 activate
     address-family ipv4 vrf vrf2
	  neighbor 2.2.0.1 remote-as 65000
      neighbor 2.2.0.1 activate
      
	```
*   This output can then be parsed by:
    *   Remove newlines to get a single line of string
    *   Replace "router" with "\nrouter" to separate bgp routers per line
    *   Find the line that matches required router bgp {{ID}}
    *   Take that line and replace "address-family" with "\naddress-family" to get address-family neighbors per line

### <a name="writers1"></a>Writers



*   A writer needs to implement all 3 methods: Write, Update, Delete in order to fully support default rollback mechanism of the framework
    *   Time showed that update like 1. delete, 2. write is anti-pattern and should not be used.
*   A writer can properly work only if there is a reader for the same composite node
*   A writer should check whether the command it executed was handled by the device properly (by checking the output) and if not throw one of the Write/Update/Delete FailedException
*   **Chunk templating framework is preferred to use in writers** it gives us:
    *   Null safety
    *   if/loop etc. inside templates
    *   Default values and many more
*   **Use full version of commands** e.g. _configure terminal_ instead of _conf t_


#### <a name="mandatory-interfaces-to-implement2"></a>Mandatory interfaces to implement

Each writer needs to implement one of these interfaces based on type of target node in YANG. Unlike mandatory interfaces for reading, only interfaces for writing config data are available (because it is not possible to write operational data). These interfaces also contain util methods which may be used for better manipulation with data. For more information about methods please read javadocs.

All writers override updateCurrentAttributes method and avoid delete/write combination, unless specified in a comment.

**CliListWriter** - implement this interface if target composite node in YANG is list. An implementation needs to be registered as GenericListWriter.

**CliWriter** - implement this interface if target composite node in YANG is container or augmentation. An implementation needs to be registered as GenericWriter.

**CompositeWriter** - extend this abstract class when multiple writers need to be invoked on one YANG node. The writers need to have a check whether or not should they be invoked.

#### <a name="existing-noop-writers2"></a>Existing noop writers

Noop writers may be registered in case when target node in YANG does not contain any simple nodes (leafs).

**NoopCliListWriter** - register as GenericListWriter if target composite node in YANG is list.

**NoopCliWriter** - register as GenericWriter if target composite node in YANG is container.


### <a name="translateunit1"></a>TranslateUnit

Translate unit class must implement interface [TranslateUnit](https://gerrit.frinx.io/plugins/gitblit/blob/?f=translation-registry-spi/src/main/java/io/frinx/cli/registry/spi/TranslateUnit.java&r=cli.git&h=carbon/development). Naming convention for translate unit class is device-type+openconfig-domain+Unit (e.g. IosXrInterfaceUnit). Translate unit class is usually instantiated, initialized and closed from Blueprint.

Implementation of TranslateUnit must be registered into _TranslationUnitCollector_ and must specify device type and device version during registration. Snippet below shows registration of [IosXRInterfaceUnit](https://github.com/FRINXio/cli-units/blob/master/ios-xr/interface/src/main/java/io/frinx/cli/unit/iosxr/ifc/IosXRInterfaceUnit.java) for device type "ios xr" all versions starting with "5".


```
    private final TranslationUnitCollector registry;
    private TranslationUnitCollector.Registration reg;

    public static final Device IOS_5 = new DeviceIdBuilder()
        	.setDeviceType("ios xr")
        	.setDeviceVersion("5.*")
        	.build();

    public IosXRInterfaceUnit(@Nonnull final TranslationUnitCollector registry) {
        this.registry = registry;
    }

    public void init() {
        reg = registry.registerTranslateUnit(IOS_5, this);
    }

    public void close() {
        if (reg != null) {
            reg.close();
        }
    }
```


[Blueprint example](https://github.com/FRINXio/cli-units/blob/master/ios-xr/interface/src/main/resources/org/opendaylight/blueprint/blueprint.xml) of injecting TranslationUnitCollector to IosXRInterfaceUnit:


```
<blueprint xmlns="http://www.osgi.org/xmlns/blueprint/v1.0.0"
           xmlns:odl="http://opendaylight.org/xmlns/blueprint/v1.0.0"
           odl:use-default-for-reference-types="true">

    <reference id="translationRegistry"
               interface="io.frinx.cli.registry.api.TranslationUnitCollector"/>

    <bean id="iosXRInterfaceUnit"
          class="io.frinx.cli.unit.iosxr.ifc.IosXRInterfaceUnit"
          init-method="init" destroy-method="close">
        <argument ref="translationRegistry" />
    </bean>
</blueprint>
```


Implementation of TranslateUnit must implement these methods:

**String toString()**



*   Return unique string among all translation units which will be used as ID for the translation unit (e.g. "IOS XR Interface (Openconfig) translate unit")

**Set<YangModuleInfo> getYangSchemas()**



*   Return YANG models containing composite nodes handled by handlers(readers/writers). It must return empty Set if no handlers are implemented.

**Set<RpcService<?, ?>> getRpcs(@Nonnull Context context)**



*   Return RPC services implemented in the translation unit. Parameter _context.getTransport()_ returns _Cli_ object containing methods for communication with a device via CLI - may need to be passed to RPC implementations.

**void provideHandlers(@Nonnull ModifiableReaderRegistryBuilder rRegistry, @Nonnull ModifiableWriterRegistryBuilder wRegistry, @Nonnull Context context)**

*   Handlers(readers/writers) need to be registered in this method. Parameter _context.getTransport()_ returns _Cli_ object containing methods for communication with a device via CLI - should be passed to readers/writers. 
*   Config readers need to be encapsulated into **_GenericConfigListReader_** (if reader implements translation of YANG list) or **_GenericConfigReader_** (if reader implements translation of YANG container, augmentation). Accordingly, operational readers are encapsulated into **_GenericOperListReader_** or **_GenericOperReader_**
*   Writers are encapsulated into **_GenericListWriter_** (if writer implements translation of YANG list) or **_GenericWriter_** (if writer implements translation of YANG container, augmentation).
*   Instance-identifier in generic reader/writer must be without keys pointing to the target composite node used in implemented reader/writer.
*   Instance-identifiers for YANG container and list (not for augmentations and nodes behind augmentations) are automatically generated to _IIDs_ class (used in examples bellow) during build of openconfig project.
*   **rRegistry.add**
    *   Use when common _GenericConfigListReader_, _GenericConfigReader_, _GenericOperListReader_ or _GenericOperReader_ need to be registered.
	
```     
rRegistry.add(new GenericConfigListReader<>(IIDs.IN_INTERFACE, new InterfaceReader(cli)));


```   
*   **rRegistry.addStructuralReader**
    *   May be used when composite node does not contain any simple node. In that case unkeyed instance-identifier and builder for target composite node needs to be provided as parameters.

```
rRegistry.addStructuralReader(IIDs.INTERFACES, InterfacesBuilder.class);
```


       
*   **rRegistry.subtreeAdd**
    *   Use when a reader implementation also fills composite child nodes of target composite node. Method _subtreeAdd_ requires a set of IIDs for all handled children, the IIDs must start from the reader itself, not from root.

```
rRegistry.subtreeAdd(Sets.newHashSet(IFC_ETH_CONFIG_ROOT_ID.augmentation(Config1.class),
IFC_ETH_CONFIG_ROOT_ID.augmentation(LacpEthConfigAug.class)),
new GenericConfigReader<>(IFC_ETHERNET_CONFIG_ID, new EthernetConfigReader(cli)));
```


*   **wRegistry.add**
    *   Use when common _GenericListWriter_ or _GenericWriter_ are registered.

```
wRegistry.add(new GenericWriter<>(IIDs.IN_IN_CONFIG, new InterfaceConfigWriter(cli)));
```


*   **wRegistry.subtreeAdd**
    *   Use for writers handling data of whole composite node subtrees. This ensures that if only a child node is updated, the writer gets triggered. Method _subtreeAdd_ requires a set of IIDs for all handled children, the IIDs must start from the reader itself, not from root.

```
wRegistry.subtreeAddAfter(Sets.newHashSet(IFC_ETH_CONFIG_ROOT_ID.augmentation(Config1.class),
IFC_ETH_CONFIG_ROOT_ID.augmentation(LacpEthConfigAug.class)),
new GenericWriter<>(IFC_ETHERNET_CONFIG_ID, new EthernetConfigWriter(cli)), IIDs.IN_IN_CONFIG);

Note: This example uses method subtreeAddAfter instead of subtreeAdd. 
Last parameter in this method shows dependency on writer registered under IIDs.IN_IN_CONFIG.
```


*   **Ordering of writers** - writers are stored in a linear structure and are invoked in order of registration. When registering a writer a relationship with another writer or set of writers can be expressed using _addBefore, addAfter, subtreeAddBefore, subtreeAddAfter_ methods. E.g. InterfaceWriter and VRFInterfaceWriter should have a relationship: InterfaceWriter -> VRFInterfaceWriter so that first an interface is created and only then assigned to VRF. Note: VRF writer should be between them. If the order is not expressed during registration, commands might be executed on device in an unpredictable/invalid order.


# <a name="cli-init-translation-unit"></a>CLI Init Translation Unit

Init translation unit does not contain readers and writers but it only contains implementation of _TranslateUnit_. There should be only one init translation unit per device type. Purpose of the init TU is to setup CLI prompt and define rollback strategy.

The implementation of _TranslateUnit_ needs to override methods:

**SessionInitializationStrategy getInitializer(@Nonnull final RemoteDeviceId id, @Nonnull final CliNode cliNodeConfiguration)**

*   Implement and return device specific _SessionInitializationStrategy_ where:
    *   Setup device CLI terminal with attributes like width and length allowing to display infinite output.
    *   Enter desired CLI mode which will be used as default - every reader and writer gets CLI prompt in this state (e.g. EXEC mode for IOS, config mode for IOS-XR, cli mode for Junos)

**String toString()**



*   Return unique string among all translation units which will be used as ID for the registration of the translation unit (e.g. "Junos cli init (FRINX) translate unit"). 

These methods may be overridden if necessary:

**getPreCommitHook()** - method that is invoked before actual commit is written into device. For example this method can enter configuration mode.

**getCommitHook()** - method that invokes actual commit and should catch any error on commit. Also it should handle any post-commit actions when the commit was successful.

**getPostFailedHook()** - method that is invoked when commit fails. Should implement aborts or revert strategies.

Methods like _getYangSchemas, getRpcs_ should return empty sets and method _provideHandlers_ should return nothing, just use the read registry and write registry to register handlers..


# <a name="netconf-unified-translation-unit"></a>NETCONF Unified Translation Unit

Unified translation units are located in [https://github.com/FRINXio/unitopo-units](https://github.com/FRINXio/unitopo-units) repository.

Kotlin is used as prefered programming language in NETCONF translation units because it provides [type aliases](https://kotlinlang.org/docs/reference/type-aliases.html) and better [null-safety](https://kotlinlang.org/docs/reference/null-safety.html).


### <a name="readers2"></a>Readers


*   Readers are handlers responsible for reading and parsing the data coming from a device
*   There are 2 types of readers: Reader and ListReader. Reader can be used to handle container or argument nodes and ListReader should handle list nodes from YANG.
    *   Both types need to implement **_readCurrentAttributes_** to fill the builder with appropriate values
    *   ListReader needs to also implement **_getAllIds()_** where it retrieves a key for each item to be present in current list. After the list is received, framework will invoke **_readCurrentAttributes_** for each item from getAllIds
*   Readers also need to implement boilerplate methods:
    *   **_getBuilder()_** - return builder object for managed node

```
override fun getBuilder(instanceIdentifier: IID<Interface>): InterfaceBuilder = InterfaceBuilder()
```

   *   **_merge_** - cast the builder parameter to appropriate parent builder type e.g. in builder for /interfaces/interface you would perform: 

```
override fun merge(builder: Builder<out DataObject>, list: List<Interface>) {
    (builder as InterfacesBuilder).`interface` = list
}
```

#### <a name="mandatory-interfaces-to-implement3"></a>Mandatory interfaces to implement

Each reader needs to implement one of these interfaces based on type of target node in YANG.For more information about methods please read javadocs.

**ConfigListReaderCustomizer** - implement this interface if target composite node in YANG is list and represents config data.

**ConfigReaderCustomizer** - implement this interface if target composite node in YANG is container or augmentation and represents config data.

**OperListReaderCustomizer** - implement this interface if target composite node in YANG is list and represents operational data.

**OperReaderCustomizer** - implement this interface if target composite node in YANG is container or augmentation and represents operational data.


#### <a name="typed-interfaces-to-implement-optional2"></a>Typed interfaces to implement (optional)

Interfaces which you may want to implement when some parent node in instance-identifier needs be checked for particular value or other data from data tree needs to be checked.

If data did not pass check, then reader implementing the interface will not be invoked by framework. Each descended reader needs to implement the interface as well.

**TypedListReader** - use when target composite node in YANG is list

**TypedReader** - use when target composite node in YANG is container or augmentation

For example typed readers for bgp (located under _protocol_) needs to check if _identifier_ in _protocol _has value _BGP_. Otherwise readers for bgp will be invoked even if _protocol identifier_ is _OSPF_.


### <a name="writers2"></a>Writers


*   A writer needs to implement all 3 methods: Write, Update, Delete in order to fully support default rollback mechanism of the framework
    *   Time showed that update like 1. delete, 2. write is anti-pattern and should not be used.
*   A writer can properly work only if there is a reader for the same composite node
*   **Retrieve and update existing data** of device via NETCONF **in update method.** Every generated builder class has copy constructor which may be used for this purpose. It's important to keep in mind that NETCONF _dataBroker.put(..)_ method overrides existing data in device configuration.


#### <a name="mandatory-interfaces-to-implement4"></a>Mandatory interfaces to implement

Each writer needs to implement one of these interfaces based on type of target node in YANG. Unlike mandatory interfaces for reading, only interfaces for writing config data are available (because it is not possible to write operational data). For more information about methods please read javadocs.

**ListWriterCustomizer** - implement this interface if target composite node in YANG is list. An implementation needs to be registered as GenericListWriter.

**WriterCustomizer** - implement this interface if target composite node in YANG is container or augmentation. An implementation needs to be registered as GenericWriter.


#### <a name="existing-noop-writers2"></a>Existing noop writers

Noop writers may be registered in case when target node in YANG does not contain any simple nodes (leafs).

**NoopListWriter** - register as GenericListWriter if target composite node in YANG is list.

**NoopWriter** - register as GenericWriter if target composite node in YANG is container.


### <a name="translateunit2"></a>TranslateUnit

Translate unit class must implement interface [TranslateUnit](https://gerrit.frinx.io/plugins/gitblit/blob/?f=translation-registry-spi/src/main/java/io/frinx/cli/registry/spi/TranslateUnit.java&r=cli.git&h=carbon/development). Naming convention for translate unit class is just name Unit. Translate unit class is usually instantiated, initialized and closed from Blueprint.

Implementation of TranslateUnit must be registered into _TranslationUnitCollector_ and must provide set of supported underlay YANG models. Snippet below shows registration of [Unit](https://github.com/FRINXio/unitopo-units/blob/master/junos/junos-17/junos-17-interface-unit/src/main/kotlin/io/frinx/unitopo/unit/junos/interfaces/Unit.kt) for junos device version 17.3.


```
class Unit(private val registry: TranslationUnitCollector) : TranslateUnit {
    private var reg: TranslationUnitCollector.Registration? = null

    fun init() {
        reg = registry.registerTranslateUnit(this)
    }

    fun close() {
        reg?.let { reg!!.close() }
    }

    override fun getUnderlayYangSchemas() = setOf(
            UnderlayInterfacesYangInfo.getInstance())

```


[Blueprint example](https://github.com/FRINXio/unitopo-units/blob/master/junos/junos-17/junos-17-interface-unit/src/main/resources/org/opendaylight/blueprint/blueprint.xml) of injecting TranslationUnitCollector to Juniper173InterfaceUnit:


```
<blueprint xmlns="http://www.osgi.org/xmlns/blueprint/v1.0.0"
  xmlns:odl="http://opendaylight.org/xmlns/blueprint/v1.0.0"
  odl:use-default-for-reference-types="true">

  <reference id="unifiedTranslationRegistry"
    interface="io.frinx.unitopo.registry.api.TranslationUnitCollector"/>

  <bean id="juniper173InterfaceUnit"
    class="io.frinx.unitopo.unit.junos.interfaces.Unit"
    init-method="init" destroy-method="close">
    <argument ref="unifiedTranslationRegistry" />
  </bean>
</blueprint>
```


Implementation of TranslateUnit must implement these methods:

**toString(): String**



*   Return unique string among all translation units which will be used as ID for the translation unit (e.g. "IOS XR Interface (Openconfig) translate unit")

**getYangSchemas(): Set<YangModuleInfo!>**



*   Return YANG models containing composite nodes handled by handlers(readers/writers). It must return empty Set if no handlers are implemented.

**getUnderlayYangSchemas(): Set<YangModuleInfo!>**



*   Return YANG module informations about underlay models used in the translation unit. These YANG modules describes configuration of NETCONF capable device.

**getRpcs(underlayAccess: UnderlayAccess): Set<RpcService<, >>**



*   Return RPC services implemented in the translation unit. Parameter _underlayAccess_ represents object containing methods for communication with a device via NETCONF and should be passed to readers/writers. 

**provideHandlers(rRegistry: ModifiableReaderRegistryBuilder,**
**wRegistry: ModifiableWriterRegistryBuilder,**
**underlayAccess: UnderlayAccess): Unit**



*   Handlers(readers/writers) need to be registered in this method. _underlayAccess_ represents object containing methods for communication with a device via NETCONF and should be passed to readers/writers. 
*   How to register readers/writers is described in [CLI TranslateUnit](#translateunit)


# <a name="translation-units-for-different-device-versions"></a>Translation units for different device versions

In case of needing to implement a new [CLI Translation Unit](#cli-translation-unit) for specific version of device we create a new [TranslateUnit](#translateunit) (e.g. located in _iosxr/mpls_).

_In this case we use IOSXR4.* implementation as an example._


### <a name="device-registration"></a>Device registration

In TranslateUnit we had just created, _e.g. MplsUnitXR4.java_, we have to register device as a constant located _../iosxr/utils/IosXrDevices.java_ containing device type and version as described in [TranslateUnit](#translateunit) documentation.


```
public void init() {
    reg = registry.registerTranslateUnit(IOS_4, this);
}
```


This unit can reuse all writers/readers from existing ones, except the writer (or other handler)  we want to alter or create (in our example writer for tunnel configuration). We have to create a new writer with desired behaviour and add it into _provideWriters_ method.


```
private void provideWriters(ModifiableWriterRegistryBuilder wRegistry, Cli cli) {
…
wRegistry.add(new GenericWriter<>(IIDs.NE_NE_MP_LS_CO_TU_TU_CONFIG, new TunnelConfigWriterXR4(cli)));

```



### <a name="handlers2"></a>Handlers

In our example, the newly created writer have to implement CliWriter interface as well as all the methods mentioned in [Writers](#writers). With other handlers we proceed with same logic.

Similar process apply on every new implementation of different device version.


# How to write extensions for OpenConfig


# <a name="best-practices-for-handlers"></a>Best practices for handlers (readers/writers)

**Do not push code that contains following:**

1. Static imports
2. Commented out code
3. Reflection
4. Trailing whitespaces or tabs
5. Double blank lines

**Before pushing the code make sure:**

1. New classes/interfaces have the correct license header 
2. New classes/interfaces/yang model have correct date
3. All new dependencies and imports are actually used
4. All variables/methods are actually used
5. All defined exceptions can be thrown from the code
6. Comments are appropriate to the code behavior
7. Code has correct spacing
8. All comments are in English

*   Constants 
    *   Chunk 
    *   Show commands
    *   java regexes
