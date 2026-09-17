# Public transformation methodology

## Source

The source is a dated Geofabrik Indonesia OpenStreetMap PBF extract. A release's metadata identifies the snapshot date, PBF byte size and MD5, schema and manifest versions, manifest SHA-256, builder revision, database byte size, database SHA-256, and record counts.

## Transformation

The public transformation is:

`OSM PBF → allowlisted Phase 4F POI tags → category normalization → useful-name filtering → representative coordinate → conservative within-OSM deduplication → normalized SQLite POI database → RTree spatial index`

Only the approved 18 Phase 4F subcategories are included across six groups:

- Health: hospital, clinic, pharmacy
- Education: school, higher education
- Transport: railway station, bus terminal, ferry terminal, airport
- Public services: police, fire station, post office
- Daily needs: marketplace, supermarket
- Natural/geographic: park, beach, waterfall, peak

Records without a useful name are omitted; CekLokasi does not invent names. Nodes use their coordinates. Ways and relations use a geometry-derived representative point when possible. This coordinate represents the feature for nearby lookup and is not necessarily an entrance or centroid.

Within OSM, deduplication is conservative. Candidate representations combine only when they have the same normalized name and subcategory, different OSM element types, close coordinates, and compatible identifying fields. Contributing OSM element identities remain preserved. False-negative duplicates are preferred to merging distinct real-world places.

The resulting database stores normalized POIs and an RTree spatial candidate index. Release validation checks SHA-256, SQLite `PRAGMA quick_check`, logical POI count, RTree row count, and representation of all 18 subcategories.

## Publication and activation

Each snapshot is published as an immutable GitHub Release and anonymously downloaded into a clean location for validation. It is eligible for Production activation only after the public download, compressed and uncompressed checksums, SQLite integrity, counts, and category coverage pass. Publication failure leaves the current last-known-good snapshot active. Rollback may use only an immutable snapshot whose public source-offer assets remain available.

This artifact contains only OSM-derived data. Future non-OSM Phase 4F.1 provider datasets remain physically and logically separate.
