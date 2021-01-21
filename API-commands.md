# BioTools API commands

Some useful commands. See the [API reference](https://biotools.readthedocs.io/en/latest/api_reference.html) and the [API usage guide](https://biotools.readthedocs.io/en/latest/api_usage_guide.html) for a complete guide.

* Obtain token 

```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"username":"yourUserHere","password":"YourPasswordHere"}' \
"https://bio.tools/api/rest-auth/login/"
```

* Validate 'json' file before registering a tool:

```bash
curl -X PUT -H "Content-Type: application/json" \
-H "Authorization: Token $BIOTOOLS_ACCESS_TOKEN" \
-d @nf-core-rnaseq.json "https://bio.tools/api/tool/nf-core-rnaseq/validate/"
```

* Validate 'json' file before registering a tool or otherwise through an error:

```bash
status_code=$(curl -X PUT -H "Content-Type: application/json" -s -H "Authorization: Token $BIOTOOLS_ACCESS_TOKEN" -d @nf-core-rnaseq.json -o /dev/null -w "%{http_code}\n" "https://bio.tools/api/tool/nf-core-rnaseq")

if [[ "$status_code" -ne 200 ]] ; then
  echo "Json file contains an error, error code $status_code"  
fi
```

* Update tool with error

```bash
status_code=$(curl -X PUT -H "Content-Type: application/json" -s -H "Authorization: Token $BIOTOOLS_ACCESS_TOKEN" -d @nf-core-rnaseq.json -o /dev/null -w "%{http_code}\n" "https://bio.tools/api/tool/nf-core-rnaseq")

if [[ "$status_code" -ne 200 ]] ; then
  echo "Json file contains an error, error code $status_code"  
fi
```

* Download `json` file from a registered tool:

```bash
curl -X GET "https://bio.tools/api/tool/sarek/?format=json" > sarek.json
```


