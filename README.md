# @oasisomniverse/svelte — OASIS Svelte UI Component Library

The Svelte UI component library for the [OASIS Platform](https://oasisomniverse.one). 126 components covering avatar SSO, karma, NFTs, quests, map, seeds, messaging, OApps, providers and more — ready to use in any Svelte or SvelteKit project.

[![npm](https://img.shields.io/npm/v/@oasisomniverse/svelte)](https://www.npmjs.com/package/@oasisomniverse/svelte)
[![Live Demo](https://img.shields.io/badge/demo-live-brightgreen)](https://oportal.oasisomniverse.one)

## Install

```bash
npm install @oasisomniverse/svelte
```

## Basic Usage

```svelte
<script>
  import { Login, AvatarConnect, KarmaToast } from '@oasisomniverse/svelte';

  const config = { apiUrl: 'https://api.web4.oasisomniverse.one' };

  function handleLogin(event) {
    console.log('Avatar logged in:', event.detail);
  }
</script>

<Login {config} on:success={handleLogin} />
<AvatarConnect {config} on:login={handleLogin} on:logout={() => console.log('logged out')} />
<KarmaToast message="Quest completed" amount={150} />
```

All components accept a `config` prop `{ apiUrl: string }`. Omit it to use the default API endpoint.

---

## Component Reference

### Auth & Identity

#### `<Login>`

Avatar login popup/form.

```svelte
<Login
  {config}
  on:success={(e) => console.log(e.detail)}
  on:close={() => {}}
/>
```

| Prop | Type | Default | Description |
|---|---|---|---|
| `config` | `{ apiUrl: string }` | default endpoint | OASIS API configuration |

| Event | `event.detail` | Description |
|---|---|---|
| `success` | `{ avatarId, username, karma }` | Dispatched on successful login |
| `close` | — | Dispatched when the popup is dismissed |

---

#### `<Signup>`

New avatar registration form.

```svelte
<Signup {config} on:success={(e) => console.log(e.detail)} on:close={() => {}} />
```

| Event | `event.detail` | Description |
|---|---|---|
| `success` | avatar data object | Dispatched on successful registration |
| `close` | — | Dispatched when dismissed |

---

#### `<AvatarConnect>`

Login/logout toggle chip — manages session state automatically.

```svelte
<AvatarConnect
  {config}
  sessionKey="oasis_session"
  on:login={(e) => console.log(e.detail)}
  on:logout={() => {}}
/>
```

| Prop | Type | Default | Description |
|---|---|---|---|
| `config` | `{ apiUrl: string }` | default endpoint | OASIS API configuration |
| `sessionKey` | `string` | `'oasis_session'` | sessionStorage key for login state persistence |

| Event | `event.detail` | Description |
|---|---|---|
| `login` | `{ avatarId, username, karma }` | Dispatched after login |
| `logout` | — | Dispatched after logout |

---

#### `<ForgotPassword>`

```svelte
<ForgotPassword {config} on:close={() => {}} />
```

---

#### `<ResetPassword>`

Password reset form — use with the token from the reset email link.

```svelte
<ResetPassword {config} token={tokenFromUrl} on:success={() => {}} />
```

| Prop | Type | Description |
|---|---|---|
| `token` | `string` | **Required.** Reset token from the email link |

---

#### `<VerifyEmail>`

```svelte
<VerifyEmail {config} token={tokenFromUrl} on:success={() => {}} />
```

---

#### `<SearchAvatars>`

```svelte
<SearchAvatars {config} on:select={(e) => console.log(e.detail)} />
```

| Event | `event.detail` | Description |
|---|---|---|
| `select` | avatar object | Dispatched when the user picks an avatar |

---

#### `<SendInvite>` / `<AcceptInvite>`

```svelte
<SendInvite {config} on:success={() => {}} />
<AcceptInvite {config} inviteCode={code} on:success={() => {}} />
```

---

### Avatar

#### `<AvatarProfile>`

```svelte
<AvatarProfile {config} avatarId="abc123" on:close={() => {}} />
```

| Prop | Type | Description |
|---|---|---|
| `avatarId` | `string` | Avatar to display — defaults to logged-in user |

---

#### `<ViewAvatar>`

```svelte
<ViewAvatar {config} avatarId="abc123" />
```

---

#### `<EditAvatar>`

```svelte
<EditAvatar {config} on:success={() => {}} on:close={() => {}} />
```

---

#### `<ViewAvatarKarma>`

```svelte
<ViewAvatarKarma {config} avatarId="abc123" />
```

---

### Karma

#### `<KarmaToast>`

Floating karma notification.

```svelte
<KarmaToast message="Quest completed" amount={150} />
```

| Prop | Type | Description |
|---|---|---|
| `message` | `string` | Reason text shown below the karma amount |
| `amount` | `number` | Karma delta — positive shown in cyan, negative in red |

---

#### `<KarmaPanel>`

```svelte
<KarmaPanel {config} on:close={() => {}} />
```

---

### Map

```svelte
<Map {config} on:close={() => {}} />
```

---

### NFT

```svelte
<NFT {config} nftId="nft-001" on:close={() => {}} />
<PurchaseNFT {config} nftId="nft-001" on:success={() => {}} on:close={() => {}} />
```

---

### OApp

```svelte
<CreateOApp {config} on:success={(e) => console.log(e.detail)} on:close={() => {}} />
<LaunchOApp {config} oappId="my-oapp" on:close={() => {}} />
```

---

### Seeds

```svelte
<Seeds {config} on:close={() => {}} />
<PayWithSeeds {config} amount={50} recipientId="abc123" on:success={() => {}} on:close={() => {}} />
```

---

### Common UI

#### `<OasisModal>`

```svelte
<OasisModal title="My Modal" accentColor="#00c8ff" on:close={() => {}}>
  <p>Modal content goes here.</p>
</OasisModal>
```

| Prop | Type | Default | Description |
|---|---|---|---|
| `title` | `string` | `''` | Modal header title |
| `accentColor` | `string` | `'#00c8ff'` | Header accent colour |

---

#### `<NavBar>`

```svelte
<NavBar {config} links={[{ label: 'Map', href: '/map' }]} />
```

---

#### `<Settings>` / `<Wallet>` / `<StarField>` / `<ComingSoon>`

```svelte
<Settings {config} on:close={() => {}} />
<Wallet {config} on:close={() => {}} />
<StarField />
<ComingSoon label="Quests" />
```

---

## Full Component List

| Group | Components |
|---|---|
| **Auth & Identity** | AcceptInvite, AvatarConnect, ForgotPassword, Login, ResetPassword, SearchAvatar, SearchAvatars, SendInvite, Signup, VerifyEmail |
| **Avatar** | AvatarProfile, AvatarWallet, EditAvatar, SearchProfiles, ViewAchievements, ViewAvatar, ViewAvatarKarma, ViewLeagues, ViewOrganizations, ViewTournaments |
| **Data Screen** | ActivityPub, AddData, EOSIO, Ethereum, Holochain, IPFS, LoadData, ManageData, MongoDB, Neo4j, OffChainManagement, SearchData, Solana, Solid, SQLite, ThreeFold |
| **Eggs** | Eggs, ManageEggs, SearchEggs, ViewEggs |
| **Game** | Game |
| **Karma** | KarmaPanel, KarmaToast, SearchKarma, ViewKarma, VoteKarma |
| **Map** | Add2DObjectToMap, Add3DObjectToMap, AddQuestToMap, DownloadMap, ManageMap, Map, PlotRouteOnMap, SearchMap, ViewGlobal3DMap, ViewHalonsOnMap, ViewOAppOnMap, ViewQuestOnMap |
| **Messages** | MenuMessage, Message, MessageContacts, Messaging |
| **Mission** | ManageMission, Mission, SearchMission, ViewMission |
| **NFT** | ContactPopupNFT, ManageNFT, NFT, PurchaseNFT, PurchaseVirtualLandNFT, SearchNFT, ViewNFT |
| **OApp** | CreateOApp, DeployOApp, DownloadOApp, EditOApp, InstallOApp, LaunchOApp, ManageOApp, OApp, SearchOApp |
| **Providers** | CompareProviderSpeeds, CrossChainManagement, ManageAutoFailover, ManageAutoReplication, ManageLoadBalancing, ManageProviders, ProviderDropdown, Providers, SearchProviders, SeedsProvider, ViewProviderStats, ViewProviders |
| **Quest** | ManageQuest, Quest, SearchQuest, ViewQuest |
| **Seeds** | DonateSeeds, ManageSeeds, PayWithSeeds, RewardSeeds, SearchSeeds, Seeds, ViewSeeds |
| **Common UI** | ComingSoon, Confirmation, Contact, HyperDrive, NavBar, ONET, ONODE, OasisModal, Settings, SideNav, StarField, Wallet |

---

## Dark Space Design System

The OASIS component library ships with the **Dark Space** design system:

- **Background**: near-black (`#0a0d14`) with subtle nebula gradients
- **Primary accent**: electric cyan (`#00c8ff`)
- **Typography**: [Orbitron](https://fonts.google.com/specimen/Orbitron) for headings, [Rajdhani](https://fonts.google.com/specimen/Rajdhani) for body text
- **Text**: always bright (`#e0f0ff` / `#fff`) — never dim or faded
- **Borders**: translucent cyan (`rgba(0,200,255,0.2)`)
- **Cards**: glassy dark panels with `backdrop-filter: blur`

Override the CSS custom properties to theme components for your own OAPP:

```css
:root {
  --oasis-bg: #0a0d14;
  --oasis-accent: #00c8ff;
  --oasis-text: #e0f0ff;
  --oasis-border: rgba(0, 200, 255, 0.2);
}
```

---

## Live Demo

The Svelte components are showcased in **[Justice League Academy](https://github.com/NextGenSoftwareUK/Justice-League-Academy-Svelte)** — a real-world OAPP built on this library.

See the full component matrix at **[oportal.oasisomniverse.one](https://oportal.oasisomniverse.one)**.

## Links

- [GitHub](https://github.com/NextGenSoftwareUK/OASIS-Svelte-UI-Component-Library)
- [npm](https://www.npmjs.com/package/@oasisomniverse/svelte)
- [OASIS API Docs](https://oasis-web4.gitbook.io/oasis-web4-docs/)
- [Developer Portal](https://oportal.oasisomniverse.one)
- [OASIS Platform](https://oasisomniverse.one)
