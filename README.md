# Notes of kpt tutorial

```
mkdir kpt-samples
cd kpt-samples/
kpt pkg get https://github.com/GoogleContainerTools/kpt/package-examples/nginx@v0.9
cd nginx
```

```
kpt pkg tree
git init
git add .
git commit -m "Pristine nginx package"
```

```
vi deployment.yaml 
kpt fn eval --image gcr.io/kpt-fn/search-replace:v0.1 -- by-path='spec.**.app' put-value=my-nginx
docker image list
git diff
```

```
cat >> Kptfile <<EOF
  mutators:
    - image: gcr.io/kpt-fn/set-labels:v0.1
      configMap:
        env: dev
EOF
vi Kptfile 
kpt fn render
```

```
kpt live init
kubectl get all -A
live apply --reconcile-timeout=15m
kubectl get all -A
git commit -m "My cusomizations"
```

```
kpt pkg update @v0.10
git status

kpt live apply --reconcile-timeout=15m
kubectl get all -A
git status
```

```
git add .
git status
git commit -m "After update to v0.10"
```

```
git log
kpt live destroy
git status
```

```
git remote add origin git@github.com:lightreader/kpt-nginx-sample.git
git push -u origin master
```
