# Lesson 4 Assignment — Styling, Flexbox, Images & Animation
## Gloss & Co. Hair Salon App

---

## Setup

### 1. Create a new Expo project

```bash
npx create-expo-app GlossAndCo
cd GlossAndCo
```

### 2. Install dependencies

```bash
npx expo install react-native-reanimated react-native-worklets-core
```

Add the Babel plugin to `babel.config.js`:

```js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
    plugins: ['react-native-worklets-core/plugin'],
  };
};
```

### 3. Create your folder structure

```
GlossAndCo/
├── App.jsx
└── screens/
    ├── ServicesScreen.jsx
    └── GalleryScreen.jsx
```

### 4. Paste this into `App.jsx`

```jsx
import { useState } from 'react';
import { View, Text, Pressable, StyleSheet } from 'react-native';
import ServicesScreen from './screens/ServicesScreen';
import GalleryScreen from './screens/GalleryScreen';

const tabs = ['Services', 'Gallery'];

export default function App() {
  const [activeTab, setActiveTab] = useState('Services');

  return (
    <View style={styles.container}>
      <View style={styles.content}>
        {activeTab === 'Services' ? <ServicesScreen /> : <GalleryScreen />}
      </View>

      <View style={styles.tabBar}>
        {tabs.map(tab => (
          <Pressable
            key={tab}
            style={[styles.tab, activeTab === tab && styles.tabActive]}
            onPress={() => setActiveTab(tab)}
          >
            <Text style={[styles.tabText, activeTab === tab && styles.tabTextActive]}>
              {tab}
            </Text>
          </Pressable>
        ))}
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1 },
  content: { flex: 1 },
  tabBar: {
    flexDirection: 'row',
    borderTopWidth: 1,
    borderTopColor: '#eee',
    backgroundColor: '#fff',
    paddingBottom: 24,
  },
  tab: {
    flex: 1,
    paddingVertical: 14,
    alignItems: 'center',
  },
  tabActive: {
    borderTopWidth: 2,
    borderTopColor: '#c9a87c',
  },
  tabText: { fontSize: 14, color: '#aaa' },
  tabTextActive: { color: '#c9a87c', fontWeight: '600' },
});
```

### 5. Paste this into `screens/ServicesScreen.jsx`

```jsx
import { ScrollView, View, Text, Image, ImageBackground, StyleSheet } from 'react-native';

const services = [
  { id: 1, name: 'Cut & Blowout',     price: '$65',  duration: '60 min',  image: 'https://images.unsplash.com/photo-1560066984-138dadb4c035?w=400' },
  { id: 2, name: 'Full Colour',        price: '$120', duration: '90 min',  image: 'https://images.unsplash.com/photo-1522337360788-8b13dee7a37e?w=400' },
  { id: 3, name: 'Balayage',           price: '$180', duration: '150 min', image: 'https://images.unsplash.com/photo-1595476108010-b4d1f102b1b1?w=400' },
  { id: 4, name: 'Deep Conditioning',  price: '$45',  duration: '30 min',  image: 'https://images.unsplash.com/photo-1527799820374-dcf8d9d4a388?w=400' },
  { id: 5, name: 'Keratin Treatment',  price: '$200', duration: '120 min', image: 'https://images.unsplash.com/photo-1576002557082-6f37e0e9a81f?w=400' },
  { id: 6, name: 'Scalp Massage',      price: '$35',  duration: '20 min',  image: 'https://images.unsplash.com/photo-1519823551278-64ac92734fb1?w=400' },
];

function ServiceCard({ item }) {
  return (
    <View style={styles.card}>
      <Image source={{ uri: item.image }} style={styles.cardImage} />
      <View style={styles.cardBody}>
        <Text style={styles.cardName}>{item.name}</Text>
        <Text style={styles.cardDuration}>{item.duration}</Text>
        <Text style={styles.cardPrice}>{item.price}</Text>
      </View>
    </View>
  );
}

export default function ServicesScreen() {
  return (
    <ScrollView style={styles.screen}>
      <View style={styles.hero}>
        <Text style={styles.heroTitle}>Gloss & Co.</Text>
        <Text style={styles.heroSubtitle}>Premium Hair Studio</Text>
      </View>

      <View style={styles.section}>
        <Text style={styles.sectionTitle}>Our Services</Text>
        <View style={styles.grid}>
          {services.map((item) => (
            <ServiceCard key={item.id} item={item} />
          ))}
        </View>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  screen: { flex: 1, backgroundColor: '#fafafa' },
  hero: { backgroundColor: '#c9a87c', padding: 24 },
  heroTitle: { fontSize: 32, fontWeight: 'bold', color: '#fff' },
  heroSubtitle: { fontSize: 15, color: '#fff', marginTop: 4 },
  section: { padding: 16 },
  sectionTitle: { fontSize: 20, fontWeight: '700', color: '#3a3a3a', marginBottom: 12 },
  grid: {},
  card: {},
  cardImage: { width: '100%', height: 120 },
  cardBody: {},
  cardName: {},
  cardDuration: {},
  cardPrice: {},
});
```

### 6. Paste this into `screens/GalleryScreen.jsx`

```jsx
import { View, Text, Image, StyleSheet, Dimensions } from 'react-native';

const photos = [
  { id: 1, uri: 'https://images.unsplash.com/photo-1522337360788-8b13dee7a37e?w=400' },
  { id: 2, uri: 'https://images.unsplash.com/photo-1560066984-138dadb4c035?w=400' },
  { id: 3, uri: 'https://images.unsplash.com/photo-1595476108010-b4d1f102b1b1?w=400' },
  { id: 4, uri: 'https://images.unsplash.com/photo-1527799820374-dcf8d9d4a388?w=400' },
  { id: 5, uri: 'https://images.unsplash.com/photo-1576002557082-6f37e0e9a81f?w=400' },
  { id: 6, uri: 'https://images.unsplash.com/photo-1519823551278-64ac92734fb1?w=400' },
  { id: 7, uri: 'https://images.unsplash.com/photo-1522337394173-0d5f5a41e9cd?w=400' },
  { id: 8, uri: 'https://images.unsplash.com/photo-1492106087820-71f1a00d2b11?w=400' },
  { id: 9, uri: 'https://images.unsplash.com/photo-1584353684765-cb3dcd0c1a91?w=400' },
];

export default function GalleryScreen() {
  return (
    <View style={styles.screen}>
      <Text style={styles.heading}>Our Work</Text>
      <View style={styles.grid}>
        <Text style={styles.placeholder}>📸 Your job to build this grid</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  screen: { flex: 1, backgroundColor: '#fafafa' },
  heading: { fontSize: 22, fontWeight: '700', color: '#3a3a3a', padding: 16 },
  grid: { padding: 16 },
  placeholder: { color: '#aaa', textAlign: 'center', marginTop: 40 },
});
```

### 7. Start the app

```bash
npx expo start --clear
```

---

## Tasks

### Task 1 — Style the service cards (StyleSheet)

In `ServicesScreen.jsx`, the `StyleSheet` at the bottom has empty style objects. Fill them in to make the cards look polished:

- White card with rounded corners (`borderRadius: 12`) and a subtle shadow
- Service name bold, at least 16pt
- Price right-aligned (`alignSelf: 'flex-end'`)
- At least 12px of padding on `cardBody`
- `resizeMode="cover"` on the `Image`

**No inline styles** — everything goes in `StyleSheet.create()`.

---

### Task 2 — Build a two-column grid (Flexbox)

Update `styles.grid` and add a `cardWrapper` so cards display in a two-column layout:

- `flexDirection: 'row'` and `flexWrap: 'wrap'` on the grid
- Each card takes up roughly half the screen width
- Consistent gap between cards

---

### Task 3 — Add a hero image (ImageBackground)

Replace the plain `<View style={styles.hero}>` with an `<ImageBackground>`:

```
https://images.unsplash.com/photo-1522337360788-8b13dee7a37e?w=800
```

- Height at least 200
- Text sits at the bottom (`justifyContent: 'flex-end'`)
- Add a dark overlay so the text is readable

---

### Task 4 — Build the photo gallery (Image + Flexbox)

In `GalleryScreen.jsx`, replace the placeholder with a real grid:

- Map over the `photos` array and render each as an `<Image>`
- 3-column grid using `flexDirection: 'row'` + `flexWrap: 'wrap'`
- Each image is square — use `Dimensions.get('window').width / 3` for the size
- `resizeMode="cover"`

---

### Task 5 — Animate the service cards (Reanimated)

Choose and implement **two** of the following:

| Option | Description |
|---|---|
| Staggered reveal | Each card enters one after another using `FadeInDown.delay(300 + index * 150).duration(500)` on the `entering` prop |
| Fade in on mount | Cards fade from opacity 0 to 1 using `useSharedValue` + `useEffect` + `withTiming` |
| Scale on press | Card scales to 0.92 on `onPressIn`, springs back on `onPressOut` using `withSpring` |
| State-driven show/hide | A "Show More" button toggles a section using `opacity` and `translateY` driven by `withTiming` |

The staggered reveal is the easiest to start with — just one prop on `Animated.View` inside your map.

---

## Checklist before submitting

- [ ] Cards have rounded corners, shadow, and internal padding
- [ ] Services display in a two-column grid
- [ ] Hero section uses `ImageBackground` with text at the bottom
- [ ] Gallery shows a 3-column grid of square images with `resizeMode="cover"`
- [ ] At least two Reanimated animations implemented on the service cards
- [ ] No `console.error` or yellow warning boxes visible in the app

---

## Submission

Push your completed project to your GitHub Classroom repo. Make sure your final commit is on the `main` branch before the deadline.
