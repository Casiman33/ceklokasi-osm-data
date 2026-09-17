# CekLokasi OSM Data

This repository distributes the OpenStreetMap-derived databases used by CekLokasi's Nearby Places feature. It is separate from the private CekLokasi application source repository.

OSM-derived databases used in CekLokasi Production are published here under the [Open Database License 1.0](https://opendatacommons.org/licenses/odbl/1-0/). Each immutable GitHub Release provides a machine-readable database, metadata, and checksums corresponding to one Production-target snapshot. A published snapshot is not Production-active unless its entry in [`snapshots/index.json`](snapshots/index.json) says so.

## Attribution and source

© [OpenStreetMap contributors](https://www.openstreetmap.org/copyright). Source extracts are obtained from [Geofabrik's Indonesia download service](https://download.geofabrik.de/asia/indonesia.html).

See [`ODbL.md`](ODbL.md) for the licence/source-offer notice and [`docs/methodology.md`](docs/methodology.md) for the public transformation methodology.

## Snapshot lifecycle

New weekly snapshot → build → validate → publish an immutable public ODbL release → anonymously verify download, checksums, integrity, and counts → only then become eligible for Production activation.

No OSM snapshot may be activated in CekLokasi Production before its public source-offer artifact is successfully published and verified. If publication or anonymous validation fails, the current last-known-good Production snapshot remains active. Rollback may point only to a snapshot whose public source-offer asset remains available.

Every OSM-derived snapshot ever activated in CekLokasi Production is retained publicly and is not deleted or overwritten during normal operation. Indefinite retention is a CekLokasi operational policy, not a claim that ODbL specifies a fixed retention period.

## Scope boundary

Release artifacts here contain only OSM-derived data. Kemenkes, Kemendikdasmen, Kemenhub, operator/GTFS, cultural, and other non-OSM authoritative datasets are not included and must remain physically and logically separate.
