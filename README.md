# Berlin Services Costs

**Note: This is an experimental work in progress.**

---

## Requirements

- [Datasette](https://datasette.io/): `brew install datasette`
- [sqlite-utils](https://datasette.io/tools/sqlite-utils): `brew install sqlite-utils`

## Run

See [docs](https://docs.datasette.io/en/stable/settings.html#configuration-directory-mode) for details.

```bash
datasette datasette/
```

## Insert new CSVs/tables into the database

```bash
sqlite-utils insert berlin_services.db {new_table_name} {path_to.csv} --csv
```

> Use `--delimiter=";"` instead of `--csv` to indicate the delimiter. CSV is implied in that case.

## Deploy

[Deployment to Vercel](https://github.com/simonw/datasette-publish-vercel)

```bash
datasette publish vercel berlin_services.db --project=berlin-services-costs -m metadata.yml --static static:static --template-dir templates/ --install=datasette-vega
```

## Todo

- [ ] figure out templating and CSS
- [x] Deployment
- [ ] Better charting
