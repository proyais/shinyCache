# shinyCache

shinyCache is a small R package that implements basic, yet fast caching for Shiny applications. This functionality is especially useful when building Shiny applications that fetch data that wont usually change during a single session. It is also useful when working with semi-long computations that could be repeated multiple times (such as returning to an initial state).

## How to use it.

Inside the Shiny app, create a reactiveValues object to serve as the cache. Use the function cache_call to compute, fetch data externally or retrieve data from the cache. Each item in the cache is unique identified by a hash number created from the parameters `cache_params`, `cache_depends` and `prefix`. See `?cache_call` for more information.

## Example

```R
cache <- reactiveValues()

output$table <- renderDataTable({
  cache_call(
    fn = long_computation,
    cache = cache,
    cache_params = list(arg1 = user_input),
    non_cache_params = list(data = mtcars),
    prefix = "table"
  )
```
