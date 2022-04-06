# Berlin Services Costs (a Datasette exploration)

This repository is an initial exploration of using [Datasette](https://datasette.io/) for a prototype that reads in CSV data, automatically creates a SQLite DB and an API and visualizes the data in form of a dashboard.

Note that the state of this repository is unfinished. Different things were explored, but nothing is finished or polished. The main outcome is this README.

---

## Requirements

You need Python in order to develop and deploy this project. In  particular we need the following two libraries:

- [Datasette](https://datasette.io/): `brew install datasette`
- [sqlite-utils](https://datasette.io/tools/sqlite-utils): `brew install sqlite-utils`

Alternatively, you can use `pip` to install the libraries.

## Development

Start a development server running on port 8001:

```bash
datasette datasette/ --reload
```

> More details on [how to configure Datasette](https://docs.datasette.io/en/stable/settings.html#configuration-directory-mode)

## How to get CSVs into Datasette

We can use `sqlite-utils` to turn a CSV into a SQLite database.

```bash
sqlite-utils insert berlin_services.db {new_table_name} {path_to.csv} --csv
```

> Use `--delimiter=";"` instead of `--csv` to indicate the delimiter. `--csv` is implied in that case.

### Open questions

- is there a solution for making this drag n drop-able?
- How to update CSVs? Can we just use the above command the overrides the previous state?

## How to create an API

When running Datasette, it automatically analyzes the SQLite database and creates an API based on the tables and columns. If you have multiple `*.db` files in your Datasette directory, they will be picked up as well.

## How to make the data explorable

Datasette provides views for exploring and filtering the data. These views might not be aesthetically pleasing, but they are powerful. We can use filters, facets, SQL queries, etc. out of the box.

Adjusting the layout is a bit tricky because of different CSS specificity issues. It might be best to remove the Datasette CSS altogether and create our own styling from scratch.

### Dashboards

Datasette provides support for simple charting. There is a plugin that enables showing the data with the Vega charting library, however it is not very customizable. We might want to opt for including our own charting library from a CDN and building something vanilla JS style at the `/dashboard` route.

## Deployment

See [Deployment to Vercel](https://github.com/simonw/datasette-publish-vercel) for details.

```bash
datasette publish vercel berlin_services.db --project=berlin-services-costs -m metadata.yml --static static:static --template-dir templates/ --install=datasette-vega
```

### Open question

- How can this be automated and continous, e.g. through a GitHub Action?

## Authentication and Authorization

Not explored, because it's not immediately obvious how this can be achieved without adding in other technologies.

## Conclusion

Datasette is a powerful tool which gets you from CSV to a full (READ) API in literally a few minutes. A minor negative point is the styling which would need to be customized, however this is not impossible.

The big issue is currently how to get authentication and authorization work. Do we want/need this for our initial prototype? If not, Datasette is a great tool that will get us results quickly.

## Contributors

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/dnsos"><img src="https://avatars.githubusercontent.com/u/15640196?v=4?s=64" width="64px;" alt=""/><br /><sub><b>Dennis Ostendorf</b></sub></a><br /><a href="https://github.com/technologiestiftung/berlin-services-costs/commits?author=dnsos" title="Code">💻</a> <a href="https://github.com/technologiestiftung/berlin-services-costs/commits?author=dnsos" title="Documentation">📖</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!

## Credits

<table>
  <tr>
    <td>
      <a src="https://citylab-berlin.org/de/start/">
        <br />
        <br />
        <img width="200" src="https://logos.citylab-berlin.org/logo-citylab-berlin.svg" />
      </a>
    </td>
    <td>
      A project by: <a src="https://www.technologiestiftung-berlin.de/">
        <br />
        <br />
        <img width="150" src="https://logos.citylab-berlin.org/logo-technologiestiftung-berlin-de.svg" />
      </a>
    </td>
    <td>
      Supported by: <a src="https://www.berlin.de/">
        <br />
        <br />
        <img width="120" src="https://logos.citylab-berlin.org/logo-berlin.svg" />
      </a>
    </td>
  </tr>
</table>