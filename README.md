# XCA REST BssidLister (Go)

BssidLister retrieves the list of Access Points and associated (B)SSIDs from [ExtremeCloud Appliance](https://www.extremenetworks.com/product/extremecloud-appliance/) (XCA) via the provided REST API and prints CSV to stdout.

It started as a rewrite of [the Python script provided by GTAC](https://gtacknowledge.extremenetworks.com/articles/How_To/How-can-I-retrieve-a-list-of-BSSIDs-from-an-XCA-controller-using-the-REST-API/), but the output of BssidLister includes way more details than the GTAC script by now.

## Branches

This project uses two defined branches:

* `master` is the primary development branch. Code within `master` may be broken at any time.
* `stable` is reserved for code that compiles without errors and is tested. Track `stable` if you just want to use the software.

Other branches, for example for developing specific features, may be created and deleted at any time.

## Dependencies

This tool uses Go modules to handle dependencies.

## Running / Compiling

Use `go run ./...` to run the tool directly or `go build -o BssidLister ./...` to compile a binary. Prebuilt binaries may be available as artifacts from the GitLab CI/CD [pipeline for tagged releases](https://gitlab.com/rbrt-weiler/xca-rest-bssidlister-go/pipelines?scope=tags).

Tested with [go1.13](https://golang.org/doc/go1.13).

## Usage

`BssidLister -h`:

```text
Available options:
  -host string
    	XCA Hostname / IP
  -port uint
    	HTTP port where XCA is listening (default 5825)
  -secret string
    	Client Secret for authentication
  -timeout uint
    	Timeout for HTTP(S) connections (default 5)
  -userid string
    	Client ID for authentication
  -version
    	Print version information and exit

All options that take a value can be set via environment variables:
  XCAHOST           -->  -host
  XCAPORT           -->  -port
  XCATIMEOUT        -->  -timeout
  XCAUSERID         -->  -userid
  XCASECRET         -->  -secret

Environment variables can also be configured via a file called .xcaenv,
located in the current directory or in the home directory of the current
user.
```

## Authentication

BssidLister uses the OAuth authentication model used by XCA's API. Authentication is possible via username/password or via API Client credentials.

## Output

BssidLister prints CSV data to stdout when no errors occur. Any exit code that is not 0 indicates an error of some sort.

The CSV output will contain the following pieces of information _per SSID_:

1. serial: AP serial number
1. model: AP hardware type
1. ip: AP IP address
1. hostname: AP hostname
1. radio: Radio index
1. band: Wireless band
1. bssid: Service BSSID
1. ssid: Service SSID
1. disabled: Indictator whether the radio is active (false) or not (true)

A header is included in the first line of the output.

## Source

The original project is [hosted at GitLab](https://gitlab.com/rbrt-weiler/xca-rest-bssidlister-go), with a [copy over at GitHub](https://github.com/rbrt-weiler/xca-rest-bssidlister-go) for the folks over there.
