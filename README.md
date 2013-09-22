samsara
=======

time-series block device - the karmic wheel of destruction

#### Create a series

Create a new series.

```
PUT http://samsara.local/series/:seriesname

{
  resolution: 1000,    // resolution of time-series data
  blocksize: 10,       // 10x resolution per underlying block
  rrd: true,           // true overwrites keys like a rrd, false lets you configure 
  retention: 86400000  // how many milliseconds to retain data (ignored if rrd=false)
}
```

Add data to the time-series. Here ```:timeblock``` must be a Unix timestamp aligned to boundaries given by ```blocksize*resolution``` when creating the series above. For example, if you want minute-resolution data (resolution = 60000) and blocks of 10 minutes (blocksize = 10), then then ```:timeblock``` must be on a 10-minute timestamp boundary with all contents falling within that boundary.

```
POST http://samsara.local/series/:seriesname/:timeblock

{
  schema: {
    dimensions: {},
    measures: {}
  },
  [
    [...]
  ]
}
```

TODO: add query interface a la OLAP cubing.
