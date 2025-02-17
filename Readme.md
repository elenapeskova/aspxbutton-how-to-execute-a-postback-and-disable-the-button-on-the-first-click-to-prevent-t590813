# Button for ASP.NET Web Forms - How to disable a button after the first click
<!-- run online -->
**[[Run Online]](https://codecentral.devexpress.com/t590813/)**
<!-- run online end -->

This example demonstrates how to create a button and disable its client-side functionality after the first click.

## Overview

Follow the steps below:

1. Create a button and handle its client-side [Click](https://docs.devexpress.com/AspNet/js-ASPxClientButton.Click) event. In the handler, do the following:

   * Call the button's [SetEnabled](https://docs.devexpress.com/AspNet/js-ASPxClientButton.SetEnabled(value)) method to disable its functionality on the client.
   * Send a postback to the server to prevent subsequent clicks.

    ```aspx
    <dx:ASPxButton runat="server" ID="btnPurchase" ClientInstanceName="btnPurchase" OnClick="btnPurchase_Click"
        Text="Complete Purchase" AutoPostBack="False" ClientEnabled="True">
        <ClientSideEvents Click="OnClick" />
    </dx:ASPxButton>
    ```

    ```js
    function OnClick(s,e){ 
        s.SetText('Purchased'); 
        s.SetEnabled(false);
        __doPostBack(s.name);
    }
    ```

2. After you call the `SetEnabled` method to disable a button, the control does not pass its disabled state to the server on a postback. In this case, you should handle the button's server-side [Click](https://docs.devexpress.com/AspNet/DevExpress.Web.ASPxButton.Click) event and set the [ClientEnabled](https://docs.devexpress.com/AspNet/DevExpress.Web.ASPxButton.ClientEnabled) property to `false`.

    ```csharp
    protected void btnPurchase_Click(object sender, EventArgs e) {
        btnPurchase.Text = "Purchased";
        btnPurchase.ClientEnabled = false;
    }
    ```

## Files to Review

* [Default.aspx](./CS/Default.aspx) (VB: [Default.aspx](./VB/Default.aspx))
* [Default.aspx.cs](./CS/Default.aspx.cs) (VB: [Default.aspx.vb](./VB/Default.aspx.vb))
