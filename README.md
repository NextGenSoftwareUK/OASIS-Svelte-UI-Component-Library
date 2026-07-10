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
</script>

<AvatarConnect />
<KarmaToast />
<Login on:loggedIn={handleLogin} on:switchTo={(e) => view = e.detail} />
```

Session state and API configuration are managed by `oasisStore` — shared across all components automatically. No config prop needed.

---

## Component Reference

### Auth & Identity

#### `<Login>`

Avatar login form. Dispatches navigation events to coordinate with your own auth flow.

```svelte
<Login
  on:loggedIn={handleLogin}
  on:switchTo={(e) => view = e.detail}
/>
```

| Event | `event.detail` | Description |
|---|---|---|
| `loggedIn` | — | Dispatched on successful login |
| `switchTo` | `'signup' \| 'forgot'` | Dispatched when the user clicks Sign Up or Forgot Password |

---

#### `<Signup>`

New avatar registration form.

```svelte
<Signup on:switchTo={(e) => view = e.detail} />
```

| Event | `event.detail` | Description |
|---|---|---|
| `switchTo` | `'login'` | Dispatched when the user clicks Sign In |

---

#### `<AvatarConnect>`

Login/logout toggle chip — fully self-contained. Manages session via `oasisStore`. No props or events required.

```svelte
<AvatarConnect />
```

---

#### `<ForgotPassword>`

```svelte
<ForgotPassword />
```

---

#### `<ResetPassword>`

```svelte
<ResetPassword />
```

---

#### `<VerifyEmail>`

```svelte
<VerifyEmail />
```

---

### Avatar

Most avatar popups accept an `open` prop and dispatch `close`:

```svelte
<ViewAvatar {open} on:close={() => open = false} />
<EditAvatar {open} on:close={() => open = false} />
<AvatarWallet {open} on:close={() => open = false} />
```

---

### Karma

#### `<KarmaToast>`

Singleton toast — render once near your app root. Triggered automatically by `$karmaToast` store when karma changes.

```svelte
<KarmaToast />
```

No props. Driven by `oasisStore`.

---

#### `<KarmaPanel>`

```svelte
<KarmaPanel {open} on:close={() => open = false} />
```

---

### Common UI

#### `<OasisModal>`

Controlled via `open` prop.

```svelte
<OasisModal {open} accentColor="rgba(59,130,246,.3)" on:close={() => open = false}>
  <p>Modal content goes here.</p>
</OasisModal>
```

| Prop | Type | Default | Description |
|---|---|---|---|
| `open` | `boolean` | `false` | Controls visibility |
| `accentColor` | `string` | `'rgba(59,130,246,.3)'` | Border/accent colour |

| Event | Description |
|---|---|
| `close` | Dispatched when backdrop or close button is clicked |

---

#### `<NavBar>`

```svelte
<NavBar />
```

---

#### `<StarField>`

```svelte
<StarField />
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

Override CSS custom properties to theme components for your own OAPP:

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
