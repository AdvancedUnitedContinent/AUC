# Suspense

- lets you display a fallback until its children have finished loading.

```
<Suspense fallback={<Loading />}>
  <SomeComponent />
</Suspense>
```

## Reference 

### Props 
- children: The actual UI you intend to render. If children suspends while rendering, the Suspense boundary will switch to rendering fallback.
- fallback: An alternate UI to render in place of the actual UI if it has not finished loading. Any valid React node is accepted, though in practice, a fallback is a lightweight placeholder view, such as a loading spinner or skeleton. Suspense will automatically switch to fallback when children suspends, and back to children when the data is ready. If fallback suspends while rendering, it will activate the closest parent Suspense boundary.
### Caveats 
- React does not preserve any state for renders that got suspended before they were able to mount for the first time. When the component has loaded, React will retry rendering the suspended tree from scratch.
- If Suspense was displaying content for the tree, but then it suspended again, the fallback will be shown again unless the update causing it was caused by startTransition or useDeferredValue.
- If React needs to hide the already visible content because it suspended again, it will clean up layout Effects in the content tree. When the content is ready to be shown again, React will fire the layout Effects again. This ensures that Effects measuring the DOM layout don’t try to do this while the content is hidden.
-React includes under-the-hood optimizations like Streaming Server Rendering and Selective Hydration that are integrated with Suspense. Read an architectural overview and watch a technical talk to learn more.


## Usage

```
<Suspense fallback={<Loading />}>
  <Albums />
</Suspense>
```

React will display your loading fallback until all the code and data needed by the children has been loaded.

In the example below, the Albums component suspends while fetching the list of albums. Until it’s ready to render, React switches the closest Suspense boundary above to show the fallback—your Loading component. Then, when the data loads, React hides the Loading fallback and renders the Albums component with data.
