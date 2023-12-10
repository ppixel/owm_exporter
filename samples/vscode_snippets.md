# Snippets for Visual Studio Code
This is a collection of some code snippets for Visual Studio Code. You can copy the snippets and add them to your own collection. A good instruction you can find [here](https://code.visualstudio.com/docs/editor/userdefinedsnippets)

## Add Entry for a metric for the Prometheus exporter
Snippet:
```json
"Metric entry for exporter": {
		"prefix": "outentry",
		"body": [
			"HELP ${1} ${2}",
			"TYPE ${1} ${3|gauge,counter,histogram,summary|}"
			"${1} ${4}",
			"${0}"
		]
	}
```
Output example:
```
HELP owm_lat Latitude of location.
TYPE owm_lat gauge
owm_lat {api_data['coord']['lat']}
```