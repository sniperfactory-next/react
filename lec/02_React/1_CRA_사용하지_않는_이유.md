# CRA 사용하지 않는 이유

create-react-app 패키지가 2022년 이후, 업데이트가 되어있지 않아서 아래와같은 호환성 이슈가 있기 때문이다. 너무 관리가 되고있지 않은 패키지이다.

```
One of your dependencies, babel-preset-react-app, is importing the
"@babel/plugin-proposal-private-property-in-object" package without
declaring it in its dependencies. This is currently working because
"@babel/plugin-proposal-private-property-in-object" is already in your
node_modules folder for unrelated reasons, but it may break at any time.

babel-preset-react-app is part of the create-react-app project, which
is not maintianed anymore. It is thus unlikely that this bug will
ever be fixed. Add "@babel/plugin-proposal-private-property-in-object" to
your devDependencies to work around this error. This will make this message
go away.
```
