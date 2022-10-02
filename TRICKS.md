# Tricks.

### K8s yaml from stdin

```
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Namespace
metadata:
  name: tricks
EOF
```

```
kubectl apply -f - <<EOF
apiVersion: v1
kind: Namespace
metadata:
  name: tricks
EOF
```

### Curl common flags

```
curl -fksSL -v -o package.zip -u username:secret -X GET "https://example.com"
```

Explanation:

- curl - trnasfer a URL
- -f - fail silently (no output at all) on server errors
- -k - insecure
- -s - silent mode (no progress ba or error message)
- -S - show an error message
- -L - redo the request on the new place on redirection
- -v - verbose (use -i to output only response headers)
- -o - output file
- -u - user creds for auth
- -X - request type
