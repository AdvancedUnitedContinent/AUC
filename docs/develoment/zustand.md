## Zustand
A small, fast and scalable bearbones state-management solution using simplified flux principles. Has a comfy API based on hooks, isn't boilerplatey or opinionated.


## Why zustand over redux?
- Simple and un-opinionated
- Makes hooks the primary means of consuming state
- Doesn't wrap your app in context providers
- Can inform components transiently (without causing - render)
## Why zustand over context?
- Less boilerplate
- Renders components only on changes
- Centralized, action-based state management


## Useage
```
const state = useBearStore()

const nuts = useBearStore((state) => state.nuts)
const honey = useBearStore((state) => state.honey)

import { create } from 'zustand'
import { useShallow } from 'zustand/react/shallow'

const useBearStore = create((set) => ({
  bears: 0,
  increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 }),
}))

// Object pick, re-renders the component when either state.nuts or state.honey change
const { nuts, honey } = useBearStore(
  useShallow((state) => ({ nuts: state.nuts, honey: state.honey })),
)

// Array pick, re-renders the component when either state.nuts or state.honey change
const [nuts, honey] = useBearStore(
  useShallow((state) => [state.nuts, state.honey]),
)

// Mapped picks, re-renders the component when state.treats changes in order, count or keys
const treats = useBearStore(useShallow((state) => Object.keys(state.treats)))

const treats = useBearStore(
  (state) => state.treats,
  (oldTreats, newTreats) => compare(oldTreats, newTreats),
)

```