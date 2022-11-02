
# Installer le bundle Webpack Encore dans une application Symfony 6

Comment installer le bundle Webpack Encore dans une application Symfony 6.


*Pré-requis* : 
- Avoir créé une application Symfony 6
- Avoir installé Node.js et npm

## Les différentes étapes 

1. **Installer le bundle webpack-encore**
    ```
    $ composer require symfony/webpack-encore-bundle
    ```
    Cela va créer un dossier *assets* dans l’application et le fichier *webpack.config.js* à la racine de l’application

2. **Installer les dépendances**
    ```
    $ npm install
    ```
    Cela va créer un dossier *node_modules*

3. **Compiler automatiquement les fichiers**
    ```
    $ npm run watch
    ```

4. **Créer le dossier build**
    ```
    $ npm run build
    ```
    Cela créé un dossier *build* dans */public*
    
5. **Gérer les images**
- Créer un dossier *images* dans le dossier */assets* créé lors de l'installation du bundle
- Configurer *webpack.config.js* pour faire le lien entre *assets* et *build* en insérant le code suivant :
``` javascript
Encore
    // ...
    .setOutPath('public/build/')

    .copyFiles({
        from: './assets/images',

        // optional target path, relative to the output dir
        to: 'images/[path][name].[ext]',

        // if versioning is enabled, add the file hash too
        //to: 'images/[path][name].[hash:8].[ext]',

        // only copy files matching this pattern
        //pattern: /\.(png|jpg|jpeg)$/
    })
```
- Importer une image dans *assets/images/*

- Relancer webpack encore
    ```
    $ npm run watch
    ```
    Cela va générer un message d'erreur dans le terminal demandant l'installation de file-loader. Suivre la procédure d'installation. Puis refaire un : 
    ```
    $ npm run watch
    ```
    Cela créé un dossier *images* dans *public/build/*, avec l'image dedans

- Faire référence à une image dans un template twig
    ``` twig
    {# assets/images/logo.png was copied to public/build/images/logo.png #}
    <img src="{{ asset('build/images/logo.png') }}" alt="ACME logo">

    {# assets/images/subdir/logo.png was copied to public/build/images/subdir/logo.png #}
    <img src="{{ asset('build/images/subdir/logo.png') }}" alt="ACME logo">
    ```

## Documentation Symfony

- <https://symfony.com/doc/current/frontend/encore/installation.html>
- <https://symfony.com/doc/current/frontend/encore/simple-example.html#configuring-encore-webpack>
- <https://symfony.com/doc/current/frontend/encore/copy-files.html>