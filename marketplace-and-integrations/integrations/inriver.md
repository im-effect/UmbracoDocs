---
description: >-
  Details an integration available for inriver, built and maintained by Umbraco
  HQ.
---

# inriver

This integration provides a custom product picker for selected products in the [inriver](https://www.inriver.com/) Product Information Management (PIM) system. It also includes a value converter providing a strongly typed model for rendering and a sample rendering component.

## Package Links

* [NuGet install](https://www.nuget.org/packages/Umbraco.Cms.Integrations.PIM.Inriver)
* [Source code](https://github.com/umbraco/Umbraco.Cms.Integrations/tree/main/src/Umbraco.Cms.Integrations.PIM.Inriver)
* [Umbraco marketplace listing](https://marketplace.umbraco.com/package/umbraco.cms.integrations.pim.inriver)

## Minimum version requirements

To ensure compatibility, check the **Dependencies** tab on NuGet for the required Umbraco CMS version. For example, see [Umbraco.Cms.Integrations.PIM.Inriver](https://www.nuget.org/packages/Umbraco.Cms.Integrations.PIM.Inriver#dependencies-body-tab).

## Authentication

Accessing the resources from inriver through the REST API requires an API key, which will be included with each request using the `X-InRiver-APIKey` header.

To retrieve your API key and instance of your environment, follow these steps:

1. Access your inriver account.
2. Go to the **Users** section of the **Control Center**.
3. Generate an API key.

## Configuration

The following configuration is required for working with the inriver API:

{% code title="appsettings.json" %}
```json
{
  "Umbraco": {
    "CMS": {
      "Integrations": {
        "PIM": {
          "Inriver": {
            "Settings": {
              "ApiBaseUrl": "https://[API_instance].productmarketingcloud.com/",
              "ApiKey": "[API_key]"
            }
          }
        }
      }
    }
  }
}
```
{% endcode %}

## Backoffice usage

To use the product picker, a new datatype should be created based on the `inriver Entity Picker` property editor.

If the configuration is not valid, an error message will be displayed.

Otherwise, you will be able to toggle between the **inriver** entity types of your environment and pick which columns you want to be displayed.

Select the entity type which you need to fetch data from, and retrieve the list of fields and linked entities for it.

## Front-end rendering

A strongly typed model will be generated by the property value converter. An HTML helper is available to render the product on the front end.

Make sure your template has a reference to the following using statement:

```csharp
@using Umbraco.Cms.Integrations.PIM.Inriver.Helpers;
```

Assuming a property based on the created Data Type with the alias `inriverProductPicker` has been created, render the product using:

```csharp
@Html.RenderInriverEntity(Model.InriverProductPicker)
```

You can override the sample rendering component with one of your own by specifying a new path for the view.
