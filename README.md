# QuerySmith
Accept URLs on stdin, replace all query string values with a user-supplied value, only output each combination of query string parameters once per host and path.

This tool is inspired by the qsreplace tool created by @tomnomnom. QuerySmith accepts URLs on stdin, replaces all query string values with a user-supplied value. It does not encode special characters in the user-supplied value. This means that if you include special characters like "?", "&", and "=" in the user-supplied value, they will not be URL encoded in the output.

# Install QuerySmith
` go install github.com/MayurUdiniya/QuerySmith@latest `

# Some Example Usage
```
$ cat urls.txt
http://example.com?foo=1&bar=2
http://example.com?bar=2&foo=1
http://example.com?baz=3&foo=1
http://example.com?foo=1&baz=3

$ cat urls.txt | QuerySmith "newvalue"
http://example.com?bar=newvalue&foo=newvalue
http://example.com?baz=newvalue&foo=newvalue

```
# Example Usage to inject special character inside parameter value
```
cat urls.txt
http://example.com?foo=1&bar=2
http://example.com?bar=2&foo=1
http://example.com?baz=3&foo=1
http://example.com?foo=1&baz=3

cat urls.txt | QuerySmith "newValue\${7*7}<xsspayload>'"
http://example.com?bar=newValue${7*7}<xsspayload>'&foo=newValue${7*7}<xsspayload>'
http://example.com?baz=newValue${7*7}<xsspayload>'&foo=newValue${7*7}<xsspayload>'
```

# Example Usage to append new character inside parameter value

```
echo "https://example.com/?foo=bar&key=value" | QuerySmith -a 123
https://example.com/?foo=bar123&key=value123
```



