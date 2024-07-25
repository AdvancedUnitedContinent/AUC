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
