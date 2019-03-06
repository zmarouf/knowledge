# Database Migrations

Good POV
>Something I understood only recently is that a DB is an API. You can add fields/tables to it easily but changes should always be backwards-compatible (if you care about availability). Only when all the clients have been upgraded can the old fields/tables be removed.
>
>Most deploys should be:
>
>1. Adding fields/tables
>2. Replace all clients
>3. Remove old fields/tables
>
>In the case of a rename triggers should be used to duplicate data between step 1 and 3.

Other POV
>Adopting three rules has pretty much made migrations a non issue:
>
>1. Migrations should be timestamped, tracked, and applied in time order (rails-style migrations; this allows for the migrator to determine which migrations have not been applied regardless of when they get added to the run list)
>2. Migrations should be committed separate from logic changes (this way you can bring in migration a if migration b depends on it even when feature a isn't ready to be merged) 
>3. Migrations are always forward. It's great to be able to revert during development but production is always forward. If a migration fails it always requires investigation; there is no automatic recovery.
>
>Using the above rules you can put together a migration system in any language in about an hour by simply storing files that issue DDL/SQL directly. With a few hours more work you can abstract it out and be cross-database but that's rarely worth it.
>
>I've tried sequentially versioned migrations and they are a major bear to work with when branching and multiple developers are involved. You end up having one guy be the "database migration guy" and responsible for keeping everything in order.
>
>The intelligent migrators that do diffs of the schema vs the db always have issues plus the very real potential to lose data.

* Using gh-ost with Aurora MySQL [link](https://www.percona.com/blog/2018/06/07/using-gh-ost-with-amazon-aurora-for-mysql/)
* Rails migrations without Rails [link](https://github.com/thuss/standalone-migrations)
