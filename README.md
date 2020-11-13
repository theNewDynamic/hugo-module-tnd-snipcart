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

### Front Matter
```yaml
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
### Some Partial/Feature

#### Examples

### Settings

Settings are added to the project's parameter under the `tnd_snipcart` map as shown below.

```yaml
# config.yaml
params:
  tnd_snipcart:
    api_key: MTkz................A3MTI2
    front_matter_key: sales
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

#### Configure Key 1

#### Configure Key 2

#### Defaults

ld copy/paste the above to your settings and append with new extensions.

## theNewDynamic

This project is maintained and love by [thenewDynamic](https://www.thenewdynamic.com).