# CB Online Linking API

> CB Online Linking API

To be able to determine the link to a dynamic page irregardless of its language, there is an api endpoint available that either redirects or provides redirect information based on a query.



## Get a specific product

### HTTP Request

`GET https://{ONLINE-HOST}/{LANGUAGE}/link/product/{CBIS-PRODUCT-ID}?format={FORMAT}`

### Query Parameters

Parameter | Description
--------- | -----------
ONLINE-HOST | the subdomain linked to Visit
LANGUAGE | two letter language-string
CBIS-PRODUCT-ID | The product-id.
FORMAT | string, json or xml

<aside class="notice">
If no format is provided, the response of the query will be a redirect to the product-page.
</aside>

> Example of response:

JSON
```json
{
Url: "http://www2.visittheuniverse.com/en/accommodation/a55221/planet-earth-hotel/details",
Name: "Planet Earth Hotel",
Id: 55221
}
```

XML
```xml
<ProductUrl xmlns="http://schemas.datacontract.org/2004/07/Online3.ViewModels.ProductLink" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
<Id>55221</Id>
<Name>Planet Earth Hotel</Name>
<Url>
http://www2.visittheuniverse.com/en/accommodation/a55221/planet-earth-hotel/details
</Url>
</ProductUrl>
```

## Get a supplier package

### HTTP Request


`GET http://{ONLINE-HOST}/{LANGUAGE}/link/packagelight/{SUPPLIER-PACKAGE-ID}?format={FORMAT}`

### Query Parameters

Parameter | Description
--------- | -----------
ONLINE-HOST | the subdomain linked to Visit
LANGUAGE | two letter language-string
SUPPLIER-PACKAGE-ID | The Id of the package
FORMAT | string, json or xml

<aside class="notice">
If no format is provided, the response of the query will be a redirect to the product-page.
</aside>

> Example of response:
 
JSON
```json
{
Url: "http://www2.visittheuniverse.com/sv/boende/a1234/br%c3%b6sarps-g%c3%a4stgifveri-%26-spa/pl22233/supplierpackagedetails/my-weekend?propertyId=ptg-1111",
Name: "My Weekend package",
Id: 22233
}
```

XML
```xml
<ProductUrl xmlns="http://schemas.datacontract.org/2004/07/Online3.ViewModels.ProductLink" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
<Id>22233</Id>
<Name>My Weekend package</Name>
<Url>
http://www2.visittheuniverse.com/sv/boende/a1234/br%c3%b6sarps-g%c3%a4stgifveri-%26-spa/pl22233/supplierpackagedetails/my-weekend?propertyId=ptg-1111
</Url>
</ProductUrl>
```

 