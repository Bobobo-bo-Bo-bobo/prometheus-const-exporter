**__Note__**: Because I'm running my own servers for serveral years, all data and repositories are hosted there
at <https://git.ypbind.de/cgit/prometheus-const-exporter/about/>

---

Export (predefined) constant values for Prometheus
==================================================
## Preface
In some cases it is required to also report semi constant (that may only change in
long, predefined intervals) values for [Prometheus](https://prometheus.io) to scrape, for instance
to display resource utilisation.

---

## Method of operation
[prometheus-const-exporter](https://git.ypbind.de/cgit/prometheus-const-exporter/) reads the constant values
and possible labels from it's configuration file. It listens (default: on all interfaces on port 19999) for
HTTP requests and export the configured constants when `/metrics` is queried by the Prometheus scraper.

On every request for `/metrics` the configuration file is read and parsed, hence the configured values
can be updated on the fly.

---

## Build requirements
### Go!
Obviously because the exporter has been written in [Go](https://golang.org/).

### Go package - github.com/go-ini/ini
Parsing the INI format of configuration is done using the [github.com/go-ini/ini](https://github.com/go-ini/ini) package

---

## Configuration
The configuration file is a INI file. Except for the default section the names of the sections doesn't matter as long
as they are unique.

### DEFAULT section
If the first section name is omitted it will be threated as the default section named `DEFAULT` and contain metric
labels exported to _all_metrics.

### Sections
Section names beside the default section (`DEFAULT`) doesn't matter, although the should be unique.
All options in the section are label name and there values exported to Prometheus *except* the reserved
option `value` which _*must*_ be a number and represents the metrics value to be exported.

Sections can override defaults by setting the corresponding key to new value inside the section.

---

## Example configuration
An example configuration file can be found in the `etc` directory of this package.

---

## Command line parameters
prometheus-const-exporter supports the following command line parameters:

  * `-config-file` - location of the configuration file, default: `/etc/prometheus/prometheus-const-exporter.ini`
  * `-help` - displays a short help text
  * `-listen-address` - address to listen for requests, default: `:19999`

---

## License
This program is licenses under [GLPv3](http://www.gnu.org/copyleft/gpl.html).

