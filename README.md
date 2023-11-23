[![No Maintenance Intended](http://unmaintained.tech/badge.svg)](http://unmaintained.tech/)

# DEPRECATED ⛔️
This package is no longer maintained.

# Vue Image Tags
Vue image tags is a plugin to create tags on images. 

## Demo
![demo-gif](https://user-images.githubusercontent.com/16884249/102064540-405eef00-3e19-11eb-92aa-e08244c7ee9e.gif)


## Installation
```bash
npm install vue-image-tags --save
```

## Usage
Register the vue-image-tags components

#### ES6

```bash
import { VueitInputImage, VueitTaggedImage } from 'vue-image-tags'

export default {
  ...
  components: {
    VueitInputImage,
    VueitTaggedImage
  },
  ...
}
```

### Tag Input
After that, you can use them in your templates. For taking tag inputs on an image, we use the `vueit-input-image` compnent.
```bash
<vueit-input-image :src="imageSrc" />
```

This component emits the `@modify` event with the `tags` as its payload whenever you add, delete or update tags. The payload contains information about each tag along with it's x coordinate and y coordinate which are converted to percentages from top left of the image instead pixels for respsiveness. You can use the tags from the payload in your application as required i.e saving it to database, making API calls etc.

#### Example:
```bash
<vueit-input-image :src="imageSrc" @modify="saveToDb" />

export default{
    ...
    methods: {
        saveToDb(tags){
            // Your logic here...
        }
    }
    ...
}
```

#### Props
The vueit-input-image component takes the following props

| Prop          | Type      | Required  | Default   |
| ------------- | --------- | --------- | --------- |
| src           | String    | Yes       |           |
| markerColor   | String    | No        | '#26abff' |


### Output Image with Tags

Similarly, to display a tagged image along with its tags, we use the `vueit-tagged-image` component. This components takes `tags` as its props.
```bash
<vueit-tagged-image :tags="someTags" :src="imageSrc" />

export default{
    ...
    data(){
        someTags: [
            {
                title: 'Some title',
                description: 'Some description',
                link: #,
                xCoordinate: 28.65438755664,
                yCoordinate: 69.38461952337
            },
            // More tags will go here
        ]
    }
    ...
}
```
Similar to the payload of vueit-input-image component, the xCoordinate and yCoordinate here should be converted to percentages from top left instead of pixels or other units for responsiveness.

#### Props
The vueit-tagged-image component takes the following props

| Prop          | Type      | Required  | Default   |
| ------------- | --------- | --------- | --------- |
| tags          | Array     | Yes       |           |
| src           | String    | Yes       |           |
| linkTarget    | String    | No        | '_self'   |
| markerColor   | String    | No        | '#26abff' |
