 
# <Strong>Dicas sobre desevolver apps android </Strong>


### 1 - Layout Customizados

#### 1.1 -  Como tirar o action bar

<p> Basta apenas modificar no <b> AndroidManifest.xml </b> esta linha : </p>

```xml
 android:theme="@style/AppTheme"
```

<p> que fica ta tag <b> Application </b> por essa :</p>


```xml
 android:theme="@style/Theme.AppCompat.Light.NoActionBar"
```

    
