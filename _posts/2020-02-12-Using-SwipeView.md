---
title:  "Using SwipeView in Xamarin.Forms Tizen"
search: true
categories:
  - Tizen .NET
last_modified_at: 2020-02-12
author: Jay Cho
toc: true
toc_sticky: true
---

## SwipeView in Xamarin.Forms 4.4
The new experimental [SwipeView](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.swipeview?view=xamarin-forms) control was added in the Xamarin.Forms 4.4 release. [SwipeView](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.swipeview?view=xamarin-forms) is a container control that wraps any of your controls and make them swipe-able.

See the [API documentation](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.swipeview?view=xamarin-forms) and [official guide](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/user-interface/swipeview) for detailed information.

**Note**: Depending on the platforms for which you are developing, `SwipeView` can be only used under an experimental flag. In this case, add the following line before calling `Forms.Init` in your application.

```c#
Forms.SetFlags("SwipeView_Experimental");
```

## Preparation to use SwipeView in Tizen
For most developers who use the Tizen wearable templates when creating a project in Visual Studio, update `Tizen.Wearable.CircularUI` NuGet version to `1.5.0-pre2` or above. This update brings `Xamarin.Forms` version 4.4.0.991537 to your application.
![]({{site.url}}{{site.baseurl}}/assets/images/posts/using-swipeview/solutionexplorer.png)

## Adding SwipeView to controls
Here is how to create a simple city selector sample application (see the following code). First, wrap your images with `SwipeView`. One image is the main city image, and the other is a decorative image that shows the selected status of the main image. I put `TopItems` among four directions, so that application users can swipe down the city image to invoke an action.

```xaml
<c:CirclePage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:c="clr-namespace:Tizen.Wearable.CircularUI.Forms;assembly=Tizen.Wearable.CircularUI.Forms"
             x:Class="SwipeViewSample.MainPage"             
             BackgroundColor="GhostWhite">
	<c:CirclePage.Content>
	    <StackLayout Orientation="Horizontal" Margin="0, 70, 0, 70" Spacing="15">
	        <SwipeView>
	            <SwipeView.TopItems>
	                <SwipeItems Mode="Execute">
	                    <SwipeItem Text="select"
	                               Invoked="TopItem_Invoked" />
	                </SwipeItems>
	            </SwipeView.TopItems>
	            <!-- Content -->
	            <Grid>
	                <Image Source="Boston.png" />
	                <Image x:Name="selectedImage" Source="checked.png" IsVisible="False" InputTransparent="True"/>
	            </Grid>
	        </SwipeView>
	    </StackLayout>
	</c:CirclePage.Content>
</c:CirclePage>
```

In the cs file, simply change the visible status of a `selectedImage` when the main image is swiped down.

```c#
private void TopItem_Invoked(object sender, EventArgs e)
{
        selectedImage.IsVisible = !selectedImage.IsVisible;
}
```

Let's try running the code on an emulator. 
![]({{site.url}}{{site.baseurl}}/assets/images/posts/using-swipeview/swipeview.gif)

## Example
Now, let's add more cities with `SwipeView`:
![]({{site.url}}{{site.baseurl}}/assets/images/posts/using-swipeview/swipeviews.gif)

Again, you can check out the [API documentation](https://docs.microsoft.com/en-us/dotnet/api/xamarin.forms.swipeview?view=xamarin-forms) and [official guide](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/user-interface/swipeview) to see what else you can do with `SwipeView`.
