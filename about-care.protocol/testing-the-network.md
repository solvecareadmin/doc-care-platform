# Testing the Network

### Deployment readiness checklist

Before testing and publishing the network, make sure that:

* [ ] All files and data are referenced properly in the `input.json` file.
* [ ] There are no logical errors in the referenced data.
* [ ] The `/definitions` folder and `input.json` file are packaged together into one zip file.
* [ ] The DDF and CSV files are ready for upload.
* [ ] You have the test environment details in which you want to publish the protocol. For information on how to publish a network, see [Publishing the Network](publishing-the-network.md).

### Testing the app using BrowserStack

1. Open a web browser, and then go to [https://www.browserstack.com/](https://www.browserstack.com/).
2. Sign in to your account.
3. From the homepage, navigate to **App Live**.
4. Upload the app.
5. Select the operating system, and device model.&#x20;
6. Wait for the app to load on the device, and then start testing.\
   \
   **Note:** To view event payload and analyze data flow, select the **Network** tab **>** **Enable for all traffic**, and then save the configuration.

{% hint style="info" %}
For more information on testing mobile apps in App Live, see the [BrowserStack documentation](https://www.browserstack.com/docs/app-live).
{% endhint %}
