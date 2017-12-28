<a name="API"></a>

We are working on apiary descriptions for the API methods, that will come soon ...

A description of "plain"" rules can be found at [plain rules](plain_rules.md).

Visual Rules are intended to be used by the Portal exclusively, until a new format is developed which will replace the old format eventually. So, basically, the DCA's documentation is the reference.

Notices/notifications follow the format defined in Orion (Context Broker) for "notify" actions. [Context subscriptions](https://forge.fi-ware.org/plugins/mediawiki/wiki/fiware/index.php/Publish/Subscribe_Broker_-_Orion_Context_Broker_-_User_and_Programmers_Guide#Context_subscriptions)


## API

All HTTP request must have  `application/json` as MIME type. Responses are `application/json` also. Generally, the JSON returned as response includes a `error` field with a string describing an error or `null` if everything worked fine.

Every request should send a field header for the service (`Fiware-Service`) and the subservice (`Fiware-ServicePath`) it refers to.

For service and servicepath only alphanumeric and underscore characters are allowed.

The servicepath is a set of scopes separated by "/" and has the following limitations:
* each scope must start with "/"
* 10 maximum scope levels in a path
* 50 maximum characters in each level, only alphanum and underscore allowed
* Empty scopes are not allowed, at least it has to have length 1 (excluding the "/")

Fiware-ServicePath is an optional header. It is assumed that requests without Fiware-ServicePath belongs to a root scope "/" implicitely. 

Internally to the CEP, scopes do not have a special meaning, so the entire servicepath string is used as a unit, and no operation of CEP takes into account a particular scope inside servicepath. Note this is the current behaviour, although it could change in the future to align more closely to how Orion uses service path (i.e. in a hierarchical way)

### Notifications
| Method | Path | Description|
| ------ |:-----|-----------|
| POST   | /notices | Send an event/notification to perseo|



### Rules

CRUD for "plain" rules

| Method | Path        | Description |
| ------ |:-------------|------------|
| GET    | /rules      | List all rules |
| GET    | /rules/{id} | Get rule with `name`id|
| POST   | /rules      | Add rule |
| DELETE | /rules/{id} | Delete rule with `name`id|

### Visual Rules

CRUD for Visual Rules. Originally detailed in [DCA documentation](https://colabora.tid.es/dca/SitePages/Inicio.aspx) (RESTAPI-SBC_2.6, section 6.15).

| Method | Path    |
| ------ |:--------|
| GET    | /m2m/vrules |
| GET    | /m2m/vrules/{id} |
| POST   | /m2m/vrules |
| DELETE | /m2m/vrules/{id} |
| PUT    | /m2m/vrules/{id} |

### Version
| Method | Path | Description|
| ------ |:-----|-----------|
| POST   | /version | Get version of perseo|

### Log level
| Method | Path | Description|
| ------ |:-----|-----------|
| PUT   | /admin/log?level={level} | Set log level of perseo|
| GET   | /admin/log | Get the current log level of perseo|
