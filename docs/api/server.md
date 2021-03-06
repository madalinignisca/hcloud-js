# Server

Type: `class`

Servers are virtual machines that can be provisioned.

## Functions

### \#changeName([name: string])

| Parameter | Type     | Description                 |
| --------- | -------- | --------------------------- |
| name      | `string` | The new name for the server |

Returns: `Promise<Server>`

Change the name of the server.

### \#delete()

Returns: `Promise<Action>`

Deletes the server.

### \#getActions([params: Object])

| Parameter | Type     | Description             |
| --------- | -------- | ----------------------- |
| params    | `Object` | Can be used for sorting |

Returns: `Promise<ServerActionList>`

Get an action list for this specific server.

### \#getAction(id: number)

| Parameter | Type     | Description   |
| --------- | -------- | ------------- |
| id        | `number` | The action id |

Returns: `Promise<Action>`

Get a specific action for this server.

### \#powerOn()

Returns: `Promise<Action>`

Power on a server.

### \#powerOff()

Returns: `Promise<Action>`

Cuts power to the server. You may loose data by doing this.

### \#reboot()

Returns: `Promise<Action>`

Reboots a server gracefully by sending an ACPI request.

### \#reset()

Returns: `Promise<Action>`

Same as **#powerOff()** but starts the server after powering off.

### \#shutdown()

Returns: `Promise<Action>`

Shuts down a server gracefully by sending an ACPI shutdown request.

### \#resetPassword()

Returns: `Promise<Object>`

Tells the server to reset the root password.

#### Returned object

```javascript
{
  "rootPassword": "ABC123",
  "action": // ... An Action instance
}
```

### \#enableRescue([type: string[, sshKeys: Array]])

| Parameter | Type     | Description                                                     |
| --------- | -------- | --------------------------------------------------------------- |
| type      | `string` | Can be `linux64`, `linux32` or `freebsd64` (default: `linux64`) |
| sshKeys   | `Array`  | An array of `numbers`, `strings` or [`SSHKeys`](sshkey.md)      |

Returns: `Promise<Object>`

Enables rescue mode.

#### Returned object

```javascript
{
  "rootPassword": "ABC123",
  "action": // ... An Action instance
}
```

### \#disableRescue()

Returns: `Promise<Action>`

Disable rescue mode.

### \#createImage([type: string[, description: string]])

| Parameter   | Type     | Description                       |
| ----------- | -------- | --------------------------------- |
| type        | `string` | Can be `snapshot` or `backup`     |
| description | `string` | The description for the new image |

Returns: `Promise<Object>`

Creates a new image.

#### Returned object

```javascript
{
  "image": // ... An Image instance
  "action": // ... An Action instance
}
```

### \#rebuild(image: number|string|Image)

| Parameter | Type                                      | Description                               |
| --------- | ----------------------------------------- | ----------------------------------------- |
| image     | `number`, `string` or [`Image`](image.md) | The image the server will be rebuilt from |

Returns: `Promise<Action>`

Rebuild the server from an image.

### \#changeType(type: number|string|ServerType[, upgradeDisk: boolean])

| Parameter   | Type                                                | Description                                         |
| ----------- | --------------------------------------------------- | --------------------------------------------------- |
| type        | `number`, `string` or [`ServerType`](servertype.md) | ID, name or ServerType the server should migrate to |
| upgradeDisk | `boolean`                                           | Does not upgrade the disk if false                  |

Returns: `Promise<Action>`

Changes the server type.

### \#enableBackup([backupWindow: string])

| Parameter    | Type     | Description                                                             |
| ------------ | -------- | ----------------------------------------------------------------------- |
| backupWindow | `string` | UTC time window: `22-02`, `02-06`, `06-10`, `10-14`, `14-18` or `18-22` |

Returns: `Promise<Action>`

Enables backups for this server.

### \#attachISO(iso: number|string|ISO)

| Parameter | Type                                  | Description                      |
| --------- | ------------------------------------- | -------------------------------- |
| iso       | `number`, `string` or [`ISO`](iso.md) | ISO to be attached to the server |

Returns: `Promise<Action>`

Attaches an ISO.

### \#detachISO()

Returns: `Promise<Action>`

Detach any attached ISO.

## Members

### .id

Type: `number`

### .name

Type: `string`

### .status

Type: `string`

Will be either `running`, `initializing`, `starting`, `stopping`, `off`, `deleting`, `migrating`, `rebuilding` or `unknown`.

### .created

Type: `Date`

### .publicNet

Type: [`PublicNetwork`](public-network.md)

### .serverType

Type: [`ServerType`](servertype.md)

### .datacenter

Type: [`Datacenter`](datacenter.md)

### .image

Type: [`Image`](image.md) or `null`

### .iso

Type: [`ISO`](iso.md) or `null`

### .rescueEnabled

Type: `boolean`

### .locked

Type: `boolean`

### .backupWindow

Type: `string` or `null`

### .traffic

Type: [`Traffic`](traffic.md)

### .rootPassword

Type: `string` or `null`

This variable is only set when creating a server.