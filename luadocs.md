# Functions
* [Sleep](#Sleep)
* [LogToConsole](#LogToConsole)
* [SendPacket](#SendPacket)
* [SendPacketRaw](#SendPacketRaw)
* [SendVariantList](#SendVariantList)
* [SendWorldTouch](#SendWorldTouch)
* [SendWorldTouch](#SendWorldTouch)
* [RequestJoinWorld](#RequestJoinWorld)
* [SetItemSelected](#SetItemSelected)
* [FindPath](#FindPath)
* [GetCamera](#GetCamera)
* [GetClient](#GetClient)
* [GetInventory](#GetInventory)
* [GetItemInfo](#GetItemInfo)
* [GetItemInfo](#GetItemInfo)
* [GetItemInfoList](#GetItemInfoList)
* [GetLocal](#GetLocal)
* [GetNPC](#GetNPC)
* [GetNPCList](#GetNPCList)
* [GetObjectList](#GetObjectList)
* [GetPlayer](#GetPlayer)
* [GetPlayerList](#GetPlayerList)
* [GetPlayerInfo](#GetPlayerInfo)
* [GetTile](#GetTile)
* [GetTiles](#GetTiles)
* [GetWorld](#GetWorld)
* [Hash32](#Hash32)
* [Hash64](#Hash64)
* [ChangeValue](#ChangeValue)
* [ChangeValueVariable](#ChangeValueVariable)
* [ChangeValueColor](#ChangeValueColor)
* [GetAsyncKeyState](#GetAsyncKeyState)
* [GetAsyncKeyState](#GetAsyncKeyState)
* [AttachConsole](#AttachConsole)
* [DetachConsole](#DetachConsole)
* [Encrypt](#Encrypt)
* [LoadEncrypt](#LoadEncrypt)
* [EncryptFile](#EncryptFile)
* [LoadEncryptedFile](#LoadEncryptedFile)
* [CallGlobalFunctionFromState](#CallGlobalFunctionFromState)
* [AddHook](#AddHook)
* [RemoveHook](#RemoveHook)
* [RemoveHooks](#RemoveHooks)
* [MakeRequest](#MakeRequest)
* [ImVec2](#ImVec2)
* [ImVec4](#ImVec4)
* [Choice](#Choice)
* [MultiChoice](#MultiChoice)
* [RunThread](#RunThread)
* [RunDelayed](#RunDelayed)

# Structs
* [ClientNPC](#ClientNPC)
* [ENetClient](#ENetClient)
* [InventoryItem](#InventoryItem)
* [ItemInfo](#ItemInfo)
* [NetAvatar](#NetAvatar)
* [PlayerInfo](#PlayerInfo)
* [Tile](#Tile)
* [World](#World)
* [WorldCamera](#WorldCamera)
* [WorldObject](#WorldObject)
* [TankPacket](#TankPacket)
* [Vector2](#Vector2)
* [Vector3](#Vector3)
* [Rect](#Rect)
* [ImVec2](#ImVec2)
* [ImVec4](#ImVec4)
* [Response](#Response)

# Function Examples

Format:
`return_type Function(arguments)`

`return_type` = Type of value returned by function. Void functions will not return a value.

`Function` = Function name

`arguments` = Arguments of function. If the argument is formatted as `[, type argument_name]`, the argument is optional. If there is an "OR" in an argument, that means it can be multiple types.

## Sleep

`void Sleep(int length)`

Sleep for X milliseconds

Example:
```lua
Sleep(1000) -- 1000 Ms > 1 Second
```

## LogToConsole

`void LogToConsole(string text)`

Display text in the Growtopia chat

Example:
```lua
LogToConsole("Hello World!") --Displays "Hello World" in the Growtopia System Chat
```
## SendPacket

`void SendPacket(int type, string text)`

Send a text packet to the server

Example:
```lua
SendPacket(2, "action|input\ntext|Hello World!") -- Sends the message "Hello World!"
```

## SendPacketRaw

`void SendPacketRaw(bool client, TankPacket packet, [, int flags])`

Send [TankPacket](#TankPacket) to server/client. Flags is optional, default is 1.

Example:
```lua
-- Places an item with the id at (x, y)
local function place(id, x, y)
	pkt = {}
	pkt.type = 3
	pkt.value = id
	pkt.px = math.floor(GetLocal().pos.x / 32 + x)
        pkt.py = math.floor(GetLocal().pos.y / 32 + y)
	pkt.x = GetLocal().pos.x
	pkt.y = GetLocal().pos.y
	SendPacketRaw(false, pkt)
end
```

## SendVariantList

`void SendVariantList(VariantList varlist[, int netid] [, int delay])`

Calls [VariantList](#VariantList) on client. Netid and delay are optional. Defaults: netid = -1, delay = 0

Example:
```lua
-- Creates a warning dialog on the player's screen
local function warn(text)
	local packet = {}
	packet[0] = "OnAddNotification"
	packet[1] = "interface/atomic_button.rttex"
	packet[2] = text
	packet[3] = "audio/hub_open.wav"
	packet[4] = 0
	SendVariantList(packet)
end
```

## SendWorldTouch

`void SendWorldTouch(Vector2 world_pos [, bool mousedown])`

Sends a world touch

Example:
```lua
-- Unknown use
```

## RequestJoinWorld

`void RequestJoinWorld(string world_name)`

Sends a join request to join world `world_name`. Follows the `action|join_request` packet format.

Example:
```lua
RequestJoinWorld("START") -- Requests to join the world "START"
```

## SetItemSelected

`void SetItemSelected(int id)`

Sets the selected backpack item to `id`.

Example:
```lua
SetItemSelected(5640) -- Sets the selected item to Magplant 5000 Remote.
```

## FindPath

`bool FindPath(int x, int y [, int delay])`

Pathfinds (Finds a path and follows it) to the given coordinates. Delay is optional, default delay = 20. The function will return True if a path is found, False if a path is not found.

Example:
```lua
FindPath(10, 10) -- Pathfinds to (10, 10)
```

## GetCamera

`WorldCamera GetCamera()`

Returns WorldCamera struct. What the WorldCamera does is unknown to me.

Example:
```lua
local CAMERA = GetCamera() -- Stores the WorldCamera struct in the CAMERA variable. Not sure what this does.
```

## GetClient

`ENetClient GetClient()`



Example:
```lua
local ENET_CLIENT = GetClient() -- Stores the ENetClient struct in the ENET_CLIENT variable. Not sure what this does.
```

## GetInventory

`InventoryItem[] GetInventory()`

Returns list of InventoryItem structs. These can be accessed using InventoryItem[ITEM_ID]

Example:
```lua
-- A function that will find the amount of an item by the id. If that item is not found, it will return 0.
local function findItem(id)
    for _, item in pairs(GetInventory()) do
        if item.id == id then
            return item.amount
        end    
    end
    return 0
end
```

## GetItemInfo

`ItemInfo GetItemInfo(int id OR string item_name)`

Returns ItemInfo struct by ID or Name. 

Example:
```lua
GetItemInfo("dirt").id -- Returns Item ID of dirt (Output: 2)
GetItemInfo(5640).name -- Returns Item Name of the item with the ID 5640 (Magplant 5000 Remote)
```

## GetItemInfoList

`ItemInfo[] GetItemInfo()`

Returns full list of ItemInfo structs. Not really useful.

Example:
```lua
local ITEMS = GetItemInfoList()

local function GetItemName(id) -- Function to get Item Name from ID. Not really useful since GetItemInfo(ID).name exists.
	return ITEMS[id].name
end
```

## GetLocal

`NetAvatar GetLocal()`

Returns NetAvatar struct for the local player.

Example:
```lua
GetLocal() // Local Player
GetLocal().name // Player Name
GetLocal().netid // Player NetID
GetLocal().pos.x // Position X of Player
GetLocal().pos.y // Position Y of Player
```

## GetNPC

`ClientNPC GetNPC(int npc_id)`

Returns ClientNPC struct by NPC ID. Unknown usage beyond that.

Example:
```lua
local NPC_ID = 0 -- ID of NPC, unknown
local NPC = GetNPC(NPC_ID) -- Stores ClientNPC struct within NPC variable.
```

## GetNPCList

`ClientNPC GetNPCList()`

Returns full list of ClientNPC structs. Can be indexed with NPC ID. Useful for getting list of NPC IDs.

Example:
```lua
local NPCS = GetNPCList()
local KEYS = {}
local n=0

for k,v in pairs(NPCS) do -- Stores key (NPC ID) of ClientNPC struct in KEYS array.
  n=n+1
  KEYS[n]=k
end

for _, value in pairs(KEYS) do
	print(value) -- Prints NPC ID
end
```

## GetObjectList

`WorldObject[] GetObjectList()`

Returns full list of WorldObject structs. Can be indexed with Object ID. 

Example:
```lua
-- Pathfinds to all objects in world
local function take(id)
	for _, obj in pairs(GetObjectList()) do
		if obj.id == id then
    		FindPath(math.floor(obj.pos.x / 32), math.floor(obj.pos.y / 32), 100)
		end
	end
end
```

## GetPlayer

`NetAvatar GetPlayer(int netid)`

Returns NetAvatar struct of player by netid.

Example:
```lua
-- Returns player name from netid
local function transferName(netid)
	Player = GetPlayer(netid)
	return Player.name
end
```

## GetPlayerList

`NetAvatar GetPlayerList()`

Returns list of NetAvatar structs of all players in world.

Example:
```lua
-- Prints names of all players in the current world.
for _, Player in pairs(GetPlayerList()) do
	print(Player.name)
end
```

## GetPlayerInfo

`PlayerInfo GetPlayerInfo()`

Returns local PlayerInfo

Example:
```lua
-- Returns player build and place range (if you want it for whatever reason)
GetPlayerInfo().punchrange / 32
GetPlayerInfo().buildrange / 32 
```

## GetTile

`Tile GetTile(int tile_x, int tile_y)`

Returns Tile struct of tile (x, y)

Example:
```lua
local tile = GetTile(10, 10) -- Returns tile struct of tile at (10, 10)
print(tile.fg) -- Prints foreground item id of tile
```

## GetTiles

`Tile[] GetTiles()`

Returns list of all Tile structs in current world. 

Example:
```lua
-- Finds coordinates (x, y) of tile by id in current world.
local function findTile(id)
	for _, tile in pairs(GetTiles()) do
		if tile.id == id then
			return tile.x, tile.y
		end
	end
end
```

## GetWorld

`World GetWorld()`

Returns world struct of current world

Example:
```lua
World = GetWorld()
World.name // Current World of Player
World.width // World Width
World.height // World Height
World.tilecount // World Tile Counts
World.objectcount // World Object Count
World.lastoid // World Last Oid
```

## Hash32

`int Hash32(string text [, uint32 seed])`

Returns 32byte integer proton hash of string

Example:
```lua
-- Unknown
```

## Hash64

`int Hash64(string text [, uint64 seed])`

Returns 64byte integer proton hash of string

Example:
```lua
-- Unknown
```

## ChangeValue

`void ChangeValue(string id, bool state)`

Changes internal menu state.

Example:
```lua
ChangeValue("[A] Auto collect", true) -- Enables auto collect
```

## ChangeValueVariable

`void ChangeValue()`

Changes internal variable value.

Example:
```lua
ChangeValue("[A] Farm: Item ID", 10) -- Sets Farm: Item ID to 10
```

## ChangeValueColor

`void ChangeValue()`

Changes internal variable for color.

Example:
```lua
-- Unknown usage
```

## GetAsyncKeyState

`int GetAsyncKeyState(int key OR char key)`

Unknown.

Example:
```lua
-- Unknown usage
```

## AttachConsole

`void AttachConsole()`

Attach console to Growtopia Instance.

Example:
```lua
AttachConsole() -- Attaches console to Growtopia Instance
```

## DetachConsole

`void DetachConsole()`

Detach console from Growtopia Instance.

Example:
```lua
DetachConsole() -- Detaches console to Growtopia Instance
```

## Encrypt

`void Encrypt(string text [, int key])`

Encrypts given text. Key is optional, default key = 0.

Example:
```lua
Encrypt("Hello World!", 20) -- Encrypts "Hello World!" using the key 20.
```

## LoadEncrypt

`void LoadEncrypt(string text [, int key])`

Loads encrypted text. Key is optional, default key = 0.

Example:
```lua
LoadEncrypt("ENCRYPTED TEXT HERE", 20) -- Loads encrypted string using the key 20.
```

## EncryptFile

`void EncryptFile(string file_name [, int key])`

Encrypts existing file from script list. The output will be file_name + "_enc". Key is optional, default key = 0.

Example:
```lua
EncryptFile("file.lua", 20) -- Encrypts file.lua using the key 20. The output file will be file_enc.lua.
```

## LoadEncryptedFile

`void LoadEncryptedFile()`

Loads existing encrypted file. Key is optional, default key = 0

Example:
```lua
LoadEncryptedFile("file_enc.lua", 20) -- Loads file_enc.lua using the key 20. 
```

## CallGlobalFunctionFromState

`bool, ... CallGlobalFunctionFromState(string state_name, string global_function_name, ...)`

Call global function from other state

Example:
```lua
-- Unknown usage
```

## AddHook

`void AddHook(string hook_name, string key, function)`

Adds a hook with custom key

Example:
```lua
AddHook("variant", "onvariant", HOOK_FUNCTION(VariantList var, int netid)) -- Adds hook for client calls
AddHook("sendpacket", "onsendpacket", HOOK_FUNCTION(int type, string text)) -- Adds hook for text packets sent to server
AddHook("sendpacketraw", "onsendpacketraw", HOOK_FUNCTION(TankPacket packet, int flags)) -- Adds hook for TankPackets sent to server
AddHook("processtankupdatepacket", "onprocesstankupdatepacket", HOOK_FUNCTION(TankPacket packet)) -- Adds hook for recieving raw packet from server
AddHook("worldtouch", "onworldtouch", HOOK_FUNCTION(Vector2 pos, bool mouseDown)) -- Adds hook for world touches (block touch by returning true)
AddHook("draw", "ondraw", HOOK_FUNCTION) -- Adds hook for ImGui draw (unknown usage)
AddHook("input", "oninput", HOOK_FUNCTION(int key)) -- Adds hook for input keys. Character are uppercase, view more key at https://learn.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes
```

## RemoveHook

`void RemoveHook(string key)`

Removes hook with key from database

Example:
```lua
RemoveHook("Hook") -- Removes hook with name "Hook"
```

## RemoveHooks

`void RemoveHooks()`

Removes and disable all hooks

Example:
```lua
RemoveHooks() -- Removes all hooks
```

## MakeRequest

`Response MakeRequest(string url [, string method] [, table options] [, string post_fields] [, int connection_time_out])`

Makes an HTTP request using the given inputs. Method, options, post_fields, and connection_time_out are optional. Their defaults are unknown.

Example:
```lua
-- Sends json data to a discord webhook.
URL = "Discord Url"
DATA = [[JSON Data]]
MakeRequest(URL, "POST",{["Content-Type"] = "application/json"}, DATA)
```

## ImVec2

`ImVec2 ImVec2([float x][, float y])`

Unknown usage.

Example:
```lua
-- Unknown usage
```

## ImVec4

`ImVec4 ImVec4([float x][, float y][, float z][, float w])`

Unknown usage.

Example:
```lua
-- Unknown usage
```

## Choice

`int Choice(string[] choiceTitles [, string label])`

Unknown usage. Will return nil if "Cancel" pressed. Label is optional. The default value for label is unknown.

Example:
```lua
-- Unknown usage
```

## MultiChoice

`bool[] MultiChoice(string[] choiceTitles [, bool[] choiceStates][, string label])`

Unknown usage. Will return nil if "Cancel" pressed. ChoiceStates and Label are optional. They have unknown defaults.

Example:
```lua
-- Unknown usage
```

## RunThread

`void RunThread()`

Runs a function in a thread

Example:
```lua
RunThread(function()
	LogToConsole("Hello World!") -- Runs "Hello World!" function in a thread
end)
```

## RunDelayed

`RunDelayed(function callback, int delayMS)`

Runs a function after delayMS milliseconds.

Example:
```lua
local function taylorSwift()
	print("Hello World!")
end

RunThread(taylorSwift, 5000) -- Runs "taylorSwift" function in a thread after 5 seconds (5000 milliseconds)
```

# Struct Examples

## ClientNPC
| Type | Name | Description |
|:-----|:-----|:------------|
| Number | `id` | NPC ID |
| Number | `type` | NPC Type |
| Vector2 | `position` | NPC Position |
| Vector2 | `target` | NPC Target |

## ENetClient
| Type | Name | Description |
|:-----|:-----|:------------|
| String | `address` | Client address |
| Number | `port` | Connection port |
| Number | `connectiontimer` | Connection timer |
| Number | `token` | Connection token |
| Number | `user` | Connection user |

## InventoryItem
| Type | Name | Description |
|:-----|:-----|:------------|
| Number | `id` | Item ID |
| Number | `amount` | Item amount |
| Number | `flags` | Unknown use |

## ItemInfo
| Type | Name | Description |
|:-----|:-----|:------------|
| Number | `id` | Item ID |
| String | `name` | Item name |
| String | `filename` | Sprite file name |
| Number | `rarity` | Rarity |
| Number | `breakhit` | Amount of hits to break |
| Number | `growtime` | Grow time |
| Number | `type` | Type |
| Number | `coltype` | Collidable type |
| Number | `clothingtype` | Type of clothing |
| Number | `visualstyle` | Unknown |

## NetAvatar
| Type | Name | Description |
|:-----|:-----|:------------|
| Vector2 | `pos` | Player's position |
| String | `name` | Player's name |
| Bool | `isleft` | Player is facing left |
| Number | `netid` | Player's netid |
| Number | `userid` | Player's UID |
| String | `country` | Player's country |
| Bool | `invisible` | Player is invisible |
| Bool | `mstate` | Player is mod |
| Bool | `smstate` | Player is developer |

## PlayerInfo
| Type | Name | Description |
|:-----|:-----|:------------|
| Number | `gems` | Gem count |
| Float | `punchrange` | Punch range |
| Float | `buildrange` | Build range |
| Struct | `backpack` | Backpack Data |
| Number List | `priority` | Unknown |
| Number | `selected` | Unknown |
| Number | `size` | Unknown |
| End of Struct | `N/A` | End of Backpack Data struct |

## Tile
| Type | Name | Description |
|:-----|:-----|:------------|
| Number | `fg` | Foreground Item ID |
| Number | `bg` | Background Item ID |
| Bool | `collidable` | Is collidable |
| Number | `x` | Tile X (not pos.x) |
| Number | `y` | Tile Y (not pos.y) |
| Number | `coltype` | Collidable type(?) |
| Struct | `flags` | Tile's flags. This will return nil if the tile doesn't have any extra data. |
| Bool | `flipper` | Is tile flipper(?) |
| Bool | `enabled` | Is tile enabled |
| Bool | `public` | Is tile public |
| Bool | `silenced` | Is tile silenced |
| Bool | `water` | Is tile water |
| Bool | `glue` | Is tile glue |
| Bool | `burn` | Is tile fire |
| Bool | `painted` | Is tile painted |
| End of Struct | `N/A` | End of flags struct |
| Struct | `extra` | Extra Data |
| Number | `type` | Type |
| Float | `progress` | Only used for seeds and providers, otherwise it will return nil. |
| String | `label` | Unknown, most likely used for sign text |
| Number | `owner` | Owner UID |
| Number | `flags` | Unknown |
| Number List | `admin` | List of admin UIDs |
| Number | `lastupdate` | Unknown |
| Number | `alttype` | Unknown |
| Number | `growth` | Growth |
| Number | `fruitcount` | Amount of fruit on tree |
| Number | `volume` | Unknown, most likely used for sound blocks |
| End of Struct | `N/A` | End of extra struct |

## World
| Type | Name | Description |
|:-----|:-----|:------------|
| String | `name` | World name |
| Number | `width` | World width |
| Number | `height` | World height |
| Number | `tilecount` | Tile count |
| Number | `objectcount` | Object count |
| Number | `lastoid` | Unknown |

## WorldCamera
| Type | Name | Description |
|:-----|:-----|:------------|
| Vector 2 | `pos` | Unknown |
| Vector 2 | `center` | Unknown |
| Float | `center` | Unknown |

## WorldObject
| Type | Name | Description |
|:-----|:-----|:------------|
| Number | `id` | Object Item ID |
| Vector2 | `pos` | Object pos struct |
| Number | `amount` | Object amount |
| Number | `flags` | Object flags |
| Number | `oid` | Object ID |

## TankPacket

Unique data types:
`uint8_t` - Unsigned integer (positive values only) ranging from 0 to 255.
`uint32_t` - Unsigned integer (positive values only) ranging from 0 to 4,294,967,295.

| Type | Name | Description |
|:-----|:-----|:------------|
| uint8_t | `type` | Raw packet type |
| uint8_t | `dropped` | Unknown |
| uint8_t | `padding1` |  Unknown |
| uint8_t | `padding2` | Unknown |
| Number | `netid` | NetID |
| Number | `snetid` | Second NetID (Unknown use) |
| Number | `state` | Packet state data (only known use is for a player's direction. Facing right is 32, facing left is 48.) |
| Float | `padding4` | Unknown |
| Number | `value` | Packet value data |
| Float | `x` | Position X value |
| Float | `y` | Position Y value |
| Float | `xspeed` | Unknown |
| Float | `yspeed` | Unknown |
| Number | `padding5` | Unknown |
| Number | `px` | Position X value (unknown difference from x). 90% of the time its value is -1. |
| Number | `py` | Position Y value (unknown difference from y). 90% of the time its value is -1. |
| uint32_t | `extrasize` | Unknown |

## Vector2
| Type | Name | Description |
|:-----|:-----|:------------|
| Float | `x` | Position X data |
| Float | `y` | Position Y data |

## Vector3
| Type | Name | Description |
|:-----|:-----|:------------|
| Float | `x` | Position X data |
| Float | `y` | Position Y data |
| Float | `z` | Position Z data |

## Rect
| Type | Name | Description |
|:-----|:-----|:------------|
| Float | `x` | Position X (Length) data |
| Float | `y` | Position Y (height) data |
| Float | `z` | Position Z (depth?) data |
| Float | `w` | Position W (width) data |

## ImVec2
| Type | Name | Description |
|:-----|:-----|:------------|
| Float | `x` | Position X data |
| Float | `y` | Position Y data |

## ImVec4
| Type | Name | Description |
|:-----|:-----|:------------|
| Float | `x` | Position X data |
| Float | `y` | Position Y data |
| Float | `z` | Position Z data |
| Float | `w` | Position W data |

## Response
| Type | Name | Description |
|:-----|:-----|:------------|
| String | `content` | Response content |
