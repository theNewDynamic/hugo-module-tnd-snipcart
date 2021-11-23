# Snipcart Hugo Module

(intro)

## Requirements

Requirements:
- Go 1.14
- Hugo 0.61.0


## Installation

If not already, [init](https://gohugo.io/hugo-modules/use-modules/#initialize-a-new-module) your project as Hugo Module:

```
$: hugo mod init {repo_url}
```

Configure your project's module to import this module:

```yaml
# config.yaml
module:
  imports:
  - path: github.com/theNewDynamic/hugo-module-tnd-snipcart
```

## Usage

The module principal feature is to read the Front Matter information of a given content file stored under a given key (default `product`) and use this to build the "Add to cart" form Snipcart needs in order to start the order process.

Anywhere in your template you can invoke the `tnd-snipcart/form` partial to print the form. More information about this partial usage is available below.

### Product Data
Product data is structured using the Snipcart API and defined under the content file Front Matter under the `product` key or any other key defined in the Module settings.

```yaml
# my-product.md
title: My Product
product:
  price: 17.99
  metadata:
    something: great
    somewhere: NYC
  categories:
    - something
    - somewhere
  weight: 195
  dimensions:
    width: 34
    length: 100
    height: 22
  min_quantity: 2
  max_quantity: 5
```

#### Custom Fields

In addition to default Snipcart value, user can add Custom Fields to any product. Those fields will be added to the "Add to cart" step once the customer clicks on the Buy Button.

```yaml
# my-product.md
title: My Product
product:
  [...]
  custom_fields:
    - name: Gift Note
      type: textarea
      placeholder: Enter notes here
      required: true
    - name: Hidden
      type: readonly
      value: that-value
    - name: Size
      id: size
      options:
        - S
        - M
        - L
    - name: Gift
      type: checkbox
```

### Buy Forms

The module allow user to invoke serveral different Buy Forms, each bearing their own settings. The `_default` form settings will be invoked when no settings are passed to the `tnd-snipcart/form` partial.

Following the Module settings example below:

```yaml
# params.yaml
tnd_snipcart:
  forms:
    _default:
      buy_button_text: Buy Form Defaults
      buy_button_classes: "px-4 py-2 bg-blue-500 text-white font-bold rounded"
    list:
      buy_button_text: Buy {{price}}$
      fields:
        - id: quantity
          name: Quantity
        - id: size
          name: Size
        - id: colors
          name: Coloring
    single:
      buy_button_text: Buy!
```

The `tnd-snipcart/form` partial will be used as follow:

|partial|settings used|
|---|---|
|`{{ partial "tnd-snipcart/form" $ }}`| `_default`|
|`{{ partial "tnd-snipcart/form" (dict "Page" $ "settings" list) }}`| `..._default`, `list`|

#### Forms Fields

User can preset fields to populate the forms in addition to the "Buy Button".

The field ID must match the one as set in the Product's custom field.

### Settings

Settings are added to the project's config params under the `tnd_snipcart` map as shown below.

```yaml
# config.yaml
params:
  tnd_snipcart:
    api_key: MTkz................A3MTI2
    front_matter_key: sales
    weight_unit: grams
    global:
      modal-style: side
    forms:
      # detailed above
```

#### api_key 
Your snipcart API key as a string. As this is a public Key you don't have to worry about obfuscating it from your repo.

#### front_matter_key (default: product)

By default, you should store product information under `product` key in your Front Matter. But if your project uses something else like `sale_data` or else, just set that key here.

#### weight_unit (default: grams)
Snipcart speaks in Grams, but if your editor uses Ounces, you can set this key to `ounces` and the module to convert those to grams before using the data with Snipcart.

#### global

Snipcart allow to add some limited [global configuration](https://docs.snipcart.com/v3/setup/installation#global-configurations)

For now only two are available:
- add-product-behavior
- modal-style

The `global` key takes an map of such Snipcart global config keys without their `data-config` prefix.

For example, in order to use the side modal style:

```yaml
# config.yaml
params:
  tnd_snipcart:
    [...]
    global:
      modal-style: side
```

## theNewDynamic

This project is maintained and love by [thenewDynamic](https://www.thenewdynamic.com).
