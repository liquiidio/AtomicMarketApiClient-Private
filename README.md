<div align="center">

[![Build](https://github.com/liquiidio/AtomicMarketApiClient-Private/actions/workflows/build.yml/badge.svg)](https://github.com/liquiidio/AtomicMarketApiClient-Private/actions/workflows/build.yml)
[![Deploy](https://github.com/liquiidio/AtomicMarketApiClient-Private/actions/workflows/deploy.yml/badge.svg)](https://github.com/liquiidio/AtomicMarketApiClient-Private/actions/workflows/deploy.yml)
       
</div>

# AtomicMarketApiClient

.NET and Unity3D-compatible (Desktop, Mobile, WebGL) ApiClient for AtomicMarket

 ## Usage

 The entry point to the APIs is in the AtomicMarketApiFactory. You can initialise any supported API from there.
 You can then call any endpoint from the initialised API.
 Each endpoint has its own set of parameters that you may build up and pass in to the relevant function.

 ## Examples
 ### Getting assets available for trading on the exchange
 ```csharp

async Task GettingAllTheAssets()
{
    // Initialize the v1 assets API
    var assetsApi = AtomicMarketApiFactory.Version1.AssetsApi;

    //Getting all the assets that are available for trading on the exchange.
    var assets = await assetsApi.Assets();

    // Print their IDs on the console.
    assets.Data.ToList().ForEach(a => Console.WriteLine(a.AssetId));
}

 ```
 
 ### Getting a filtered assets list that is available for trading
 ```csharp

async Task GettingFilteredAssetsList()
{
    // Initialize the v1 assets API
    var assetsApi = AtomicMarketApiFactory.Version1.AssetsApi;

    // Build up the AssetsParameters with the AssetsUriParameterBuilder
    // This can be used to fine tune the kind of results we want
    // For example, here were limiting the results to just five assets
    // More information can be found on the documentation
    var builder = new AssetsUriParameterBuilder().WithLimit(5);

    //Getting all the assets that are available for trading on the exchange.
    var assets = await assetsApi.Assets(builder);

    // Print their IDs on the console.
    assets.Data.ToList().ForEach(a => Console.WriteLine(a.AssetId));
}

 ```
 
 ### Getting an Offer
 ```csharp

async Task GetOffer(string offerId)
{

    // Initialize the v1 offers API
    var api = AtomicMarketApiFactory.Version1.OffersApi;

    // Call the offers endpoint passing the offerId as an input
    var sales = await api.Offer(offerId);

    // Access different informations about the offer using the Data property in the result
    Console.WriteLine(sales.Data.SenderName);
}

 ```
 ### Unity Examples
 
 Our unity packages come with examples to help you get started as quickly as possible.
 
An example showing the result for searching for a sale with ID #105106129

<img width="836" alt="image" src="https://user-images.githubusercontent.com/31707324/213105963-0916568e-eea2-456f-ac39-3758ad0f4514.png">

An example showing the result for searching for an auction with ID #1016310

<img width="838" alt="image" src="https://user-images.githubusercontent.com/31707324/213106315-cd67121b-adb9-4ff3-a42f-610868206921.png">
