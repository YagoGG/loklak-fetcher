# loklak-fetcher-client
JavaScript library that allows gathering tweets from [loklak's public API](loklak.org) from the client-side.

# What's loklak?
**loklak** is a platform for anonymously gathering tweets through a peer-to-peer sharing network.
Want to know more? Here you can learn more [about loklak](http://loklak.org/about.html) and its [architecture](http://loklak.org/architecture.html).

# Set-up
To add loklak-fetcher-client to your website, just download the [latest release](https://github.com/YagoGG/loklak-fetcher-client/releases/), and copy the file `src/loklak-fetcher.js` wherever you want in your web directory.  
All you have to do after that is add the script to your HTML, and you're ready to start fetching!

```html
    <script src="my/path/loklak-fetcher.js"></script>
```

# Usage

### loklakFetcher.getTweets(query, [options], callback)
Fetches tweets from the public loklak API, with the options provided.

`query`    Query string, see the *Queries* section below  
`options`  *(optional)* Object with allowed GET-attributes, see the *Options* section below  
`callback` Function called after getting the results. These are passed as the first argument, in a JSON object like [this one](http://loklak.org/api/search.json?q=loklak)

**Example**

```javascript
    var options = {
      count: 25,
      tzOffset: 60
    };

    loklakFetcher.getTweets('loklak', options, function(tweets) {
      // Do something cool!
    });
```

This example would get the last 25 tweets containing the string `loklak`, published in 2015, with an offset of 60 minutes.

## Queries
The query string can have different tokens that allow you to make a more precise search. These are natively supported by loklak's API.

| Token          | Description |
| -----          | ----------- |
| `term1 term2`  | Both `term1` and `term2` shall appear in the tweet text |
| `@user`        | The `user` must be mentioned in the message |
| `from:user`    | Only messages published by `user` |
| `#hashtag`     | The message must contain that `#hashtag` |
| `near:locaton` | Messages shall be created near `location`  |
| `since:date`   | Only messages after `date` (provided date included), in the format `<date>=yyyy-MM-dd` or `yyyy-MM-dd_HH:mm`
| `until:date`   | Only messages before `date` (provided date excluded), in the format `<date>=yyyy-MM-dd` or `yyyy-MM-dd_HH:mm`

## Options

| Option     | Default  | Description |
| ------     | -------  | ----------- |
| `count`    | 100      | The wanted number of results |
| `source`   | 'cache'  | Source for the search, can be *cache*, *backend*, *twitter* or *all* |
| `fields`   | none     | Aggregation fields for search facets, like `'created_at,mentions'` |
| `limit`    | none     | Limitation of number of facets for each aggregation |
| `tzOffset` | 0        | Offset applied on `since:`, `until:` and the date histogram (in minutes) |
| `minified` | **true** | Minify the result. **This isn't loklak's default, for performance reasons** |

# JSONP
Because of the [**Same-Origin Policy**](https://en.wikipedia.org/wiki/Same-origin_policy), this program uses [**JSONP**](https://en.wikipedia.org/wiki/JSONP). This means that an attacker could insert malicious code if he managed to modify loklak's response before it arrives to the client.  
Keep this in mind before using this library in any application that requires a minimal security.

If this is a problem for you, definitely loklak-fetcher-client isn't what you're looking for. Consider using other alternatives like [Twitter's Official API](https://dev.twitter.com/rest/public) instead.

# Credits
Thanks to [Fossasia](http://fossasia.org/) for creating loklak, and supporting Open Source.

# License
This program is under the MIT license. You can find more on the [license file](https://github.com/YagoGG/loklak-fetcher-client/blob/master/LICENSE), and get a human-readable version of what you can do and what you can't [here](http://choosealicense.com/licenses/mit/).

***
*(c) 2016 Yago González*
