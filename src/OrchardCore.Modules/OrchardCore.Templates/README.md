# Templates (OrchardCore.Templates)

The templates module allows editors to create custom Liquid templates.

## Available templates

Templates can be defined using the web editor, or in a theme. Templates are distinguished by their name. 
Orchard Core doesn't render HTML directly, but instead will usually render something called a **Shape**, which is an object that represents
the thing to render and has all the necessary data and metatada to render HTML.

When rendering a Shape, Orchard Core will eventually look for specific templates, passing the Shape to this template. Orchard Core can match with many templates
for the same Shape. This potential templates are called **Alternates**. A Shape contains a list of acceptable template names (the alternates) and will look into
providers to get the most appropriate one. For instance when rendering a Content Item of type Article, the corresponding Shape that is rendered will be configured
to look for a template that handles all articles, but also one that handles an article when used in a list, and so on.

This document provides a list of pre-defined templates that can be used when rendering shapes. It uses the internal name of a template and also the filename
in case it's provided by a Theme.

## Content templates

### Content__[ContentType]

This template is called when displaying a content item with the `Detail` display type, for instance when accessed from its own url.

#### Examples

| Template | Filename|
| --------- | ------------ |
| Content__BlogPost | Content-BlogPost.cshtml |
| Content__Article | Content-Article.cshtml |

#### Available properties

| Property | Description |
| --------- | ------------ |
| `Model.Content` | A zone shape that contains all the shapes generated by the content's parts and fields. |
| `Model.ContentItem` | Represents the current content item being rendered by the template. |
| `Model.ContentItem.Content` | A JSon object containing all the data of the content item. |

### Content_[DisplayType]__[ContentType]

This template is called when displaying a content item with a specific display type. For instance, when a content item 
is displayed in a list, the `Summary` display type is commonly used.

#### Examples

| Template | Filename|
| --------- | ------------ |
| Content_Summary__BlogPost | Content-BlogPost.Summary.cshtml |
| Content_Summary__Article | Content-Article.Summary.cshtml |

## Widget templates

### Widget__[ContentType]

This template is called when a widget is rendered on a page.

#### Examples

| Template | Filename|
| --------- | ------------ |
| Widget__Paragraph | Widget-Paragraph.cshtml |
| Widget__Blockquote | Widget-Blockquote.cshtml |

#### Available properties

| Property | Description |
| --------- | ------------ |
| `Model.Content` | A zone shape that contains all the shapes generated by the widget's parts and fields. |
| `Model.ContentItem` | Represents the current content item being rendered by the template. |
| `Model.ContentItem.Content` | A JSon object containing all the data of the content item. |
| `Model.Classes` | An array of all the classes attached to the widget. |

## Content Part templates

Each driver is free to return a shape types of its choosing but the usage is 
to render a content part using a shape with the same type name. for instance the `BodyPart`
content part will return a single shape of type `BodyPart`, but the `ListPart` returns many
shapes, one among them begin `ListPart`.

As a consequence the following list of templates use the `[ShapeType]` term where 
most of the time it will be equal to the name of the content part. The example use
common content part names for this reason.

### Properties

The properties available on a shape rendered for a content part are unique for each content
part. Please refer to each content part documentation.

### [ShapeType]

This template is called when a Content Part is rendered.

#### Examples

| Template | Filename|
| --------- | ------------ |
| BodyPart | BodyPart.cshtml |
| ListPartFeed | ListPartFeed.cshtml |

### [ShapeType]\_[DisplayType]

This template is called when a Content Part shape type is rendered in a specific display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
| BodyPart_Summary | BodyPart.Summary.cshtml |

### [ContentType]\_[DisplayType]__[PartType]

This template is called when a content part type is rendered for a given content type, with or without a given display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
| Blog__BodyPart | Blog-BodyPart.cshtml |
| LandingPage__BagPart | LandingPage-BagPart.cshtml |
| Blog_Summary__BodyPart | Blog-BodyPart.Summary.cshtml |
| LandingPage_Summary__BagPart | LandingPage-BagPart.Summary.cshtml |

### [ContentType]\_[DisplayType]__[PartName]

This template is called when a content part name is rendered for a given content type, with or without a given display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
| LandingPage__Services | LandingPage-Services.cshtml |
| LandingPage_Summary__Services | LandingPage-Services.Summary.cshtml |

### [ContentType]\_[DisplayType]\_\_[PartType]\_\_[ShapeType]

This template is called when a shape type is rendered in a given content part type for a given content type, with or without a given display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
| Blog\_\_ListPart\_\_ListPartFeed | Blog__ListPart__ListPartFeed.cshtml |
| Blog_Summary\_\_ListPart\_\_ListPartFeed | Blog__ListPart__ListPartFeed.Summary.cshtml |

### [ContentType]\_[DisplayType]\_\_[PartName]\_\_[ShapeType]

This template is called when a shape type is rendered in a given content part name for a given content type, with or without a given display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
| LandingPage\_\_Services\_\_CustomShape | LandingPage-Services-CustomShape.cshtml |
| LandingPage_Summary\_\_Services\_\_CustomShape | LandingPage-Services-CustomShape.Summary.cshtml |

## Content Field templates

Each driver is free to return a shape types of its choosing but the usage is 
to render a content field using a shape with the same type name. for instance the `TextField`
content field will return a single shape of type `TextField`, but other fields might returns many
shapes.

### Properties

The properties available on a shape rendered for a content field are unique for each content
field. Please refer to each content field documentation.

### [ShapeType]\_[DisplayType]

This template is called when a content field type is rendered in given display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
| TextField_Summary | TextField.Summary.cshtml |

### [PartType]__[FieldName]

This template is called when a content field name is rendered for a given content part type when the shape type matches the field type, with or without a given display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
|  BodyPart__Description |  BodyPart-Description.cshtml |
|  BodyPart_Summary__Description |  BodyPart-Description.Summary.cshtml |

### [ContentType]\_\_[PartName]\_\_[FieldName]

This template is called when a content field name is rendered for a given content type and content part name when the shape type matches the field type, with or without a given display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
| Blog\_\_BodyPart\_\_Description | Blog-BodyPart-Description.cshtml |
| LandingPage\_\_Services\_\_Image | LandingPage-Services-Image.cshtml |
| Blog_Summary\_\_BodyPart\_\_Description | Blog-BodyPart-Description.Summary.cshtml |
| LandingPage_Summary\_\_Services\_\_Image | LandingPage-Services-Image.Summary.cshtml |

### [FieldType]__[ShapeType]

This template is called when a content field shape type is rendered for a given content field type, with or without a given display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
| CustomField__CustomFieldSummary | CustomField-CustomFieldSummary.cshtml |
| CustomField_Summary__CustomFieldSummary | CustomField-CustomFieldSummary.Summary.cshtml |

### [PartType]\_\_[FieldName]\_\_[ShapeType]

This template is called when a content field shape type is rendered for a given content field name in a given content part type, with or without a given display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
|  BodyPart\_\_Description\_\_CustomFieldSummary| BodyPart__Description__CustomFieldSummary.cshtml |
|  BodyPart_Summary\_\_Description\_\_CustomFieldSummary| BodyPart__Description__CustomFieldSummary.Summary.cshtml |

### [ContentType]\_\_[PartName]\_\_[FieldName]__[ShapeType]

This template is called when a content field shape type is rendered for a given content field name in a given content part name in a given content type, with or without a given display type.

#### Examples

| Template | Filename|
| --------- | ------------ |
| Blog__BodyPart\_\_Description\_\_CustomFieldSummary | Blog-BodyPart-Description-CustomFieldSummary.cshtml |
| LandingPage\_\_Services\_\_Description\_\_CustomFieldSummary | LandingPage-Services-Description-CustomFieldSummary.cshtml |
| Blog_Summary\_\_BodyPart\_\_Description\_\_CustomFieldSummary | Blog-BodyPart-Description-CustomFieldSummary.Summary.cshtml |
| LandingPage_Summary\_\_Services\_\_Description\_\_CustomFieldSummary | LandingPage-Services-Description-CustomFieldSummary.Summary.cshtml |

## Shape differentiators

The differentiator identifies uniquely a shape in a zone. When rendering a content item, the shape has a `Content` property that contains
all the shapes provided by content display drivers, including the ones for content parts and content fields.

Differentiators can be used to configure the placement information (c.f. [Placement documentation page](#)), or to access specific shapes in a zone using these template helpers:

### Content Part differentiator

If the shape type is the same as the content part name, the shape will be named `[PartName]`, e.g. `BodyPart`, `Services`.
If the shape type is different than the content part name, it will be `[PartName]-[ShapeType]`, e.g. `ListPart-ListPartFeed`

### Content Field differentiator

If the shape type is the same as the content field name, the shape will be named `[PartName]-[FieldName]`, e.g. `BodyPart-Description`, `Services-Image`.
If the shape type is different than the content field name, it will be `[PartName]-[FieldName]-[ShapeType]`, e.g. `BodyPart-Description-CustomFieldSummary`, `Services-Image-ImageFieldSummary`

#### Razor

Access a specific shape by name
```
Model.Content.BodyPart
```

Removing a specific shape by name
```
Model.Content.Remove("BodyPart");
```

#### Liquid

Display a shape after removing a specific shape by name
```
{% display Model.Content | remove_item: "BodyPart" %}
```

Display a specific shape by name
```
{% display Model.Content.BodyPart %}
```