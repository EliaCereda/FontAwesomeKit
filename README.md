FontAwesomeKit
==============

Simple helper for using Font-Awesome on iOS.

![image](https://raw.github.com/PrideChung/FontAwesomeKit/master/screenshot.png)

##What is Font-Awesome
[Font-Awesome](http://fortawesome.github.com/Font-Awesome/) is a set of iconic fonts used in Twitter Bootstrap.

##Installation

###via CocoaPods (recommended)

Add this line in your Podfile, then run `pod update`

`pod FontAwesomeKit`

###Manully

Download source code, then drag the folder `FontAwesomeKit` into your project, add CoreText framework to you project.

##Example Usage



###Using Font-Awesome on UIBarButtonItem

```objective-c
self.configBarButton.title = FAKIconCog;
[self.configBarButton setTitleTextAttributes:@{UITextAttributeFont:[FontAwesomeKit fontWithSize:24]} forState:UIControlStateNormal];
```

###Get an UIImage of an icon so you can use it on tabbar

```objective-c
UIImage *tabBarIcon = [FontAwesomeKit imageForIcon:FAKIconHeart
										 imageSize:FAKImageSizeTabbar
										  fontSize:29
										attributes:nil];
self.tabBarItem.image = tabBarIcon;
self.tabBarItem.title = @"Title you like";
```

###Get a linear gradient pattern image

```objective-c
// Notice that we use CGColor here like using CAGradientLayer
NSArray *colors = @[(id)[UIColor colorWithHue:59.0/360 saturation:0.2 brightness:1.0 alpha:1.0].CGColor,
				 (id)[UIColor colorWithHue:59.0/360 saturation:1.0 brightness:1.0 alpha:1.0].CGColor,
				 (id)[UIColor colorWithHue:59.0/360 saturation:0.8 brightness:0.8 alpha:1.0].CGColor];
// Gradient stops, from 0.0 to 1.0, values must be monotonically increasing
NSArray *locations = @[@0.2, @0.8, @1.0]; 
UIImage *gradientPattern = [FontAwesomeKit linearGradientImageWithSize:CGSizeMake(37, 37)
																colors:colors
															 locations:locations]; 
```
####Related methods
```objective-c
+ (UIImage *)linearGradientImageWithSize:(CGSize)size
								  colors:(NSArray *)colors
							   locations:(NSArray *)locations
							  startPoint:(CGPoint)startPoint
								endPoint:(CGPoint)endPoint;
```
Gives you control about where to start and stop the gradient.


```objective-c
+ (UIImage *)linearGradientImageWithSize:(CGSize)size
								  colors:(NSArray *)colors;
```
Omit the locations parameter, the first color in colors is assigned to location 0, the last color in colors is assigned to location 1, and intervening colors are assigned locations that are at equal intervals in between.

###Get a radial gradient pattern image
```objective-c
NSArray *colors = @[(id)[UIColor colorWithHue:111.0/360 saturation:1.0 brightness:1.0 alpha:1.0].CGColor,
		        (id)[UIColor colorWithHue:111.0/360 saturation:1.0 brightness:0.7 alpha:1.0].CGColor,
		];
CGPoint centerPoint = CGPointMake(45.0/2 - 5, 45.0/2);
gradientPattern = [FontAwesomeKit radialGradientImageWithSize:CGSizeMake(45, 45)
													   colors:colors // Gradient colors
													locations:locations // Gradient stops
												  startCenter:centerPoint // The coordinate that defines the center of the starting circle.												  startRadius:1.0 // The radius of the starting circle.
													endCenter:centerPoint // The coordinate that defines the center of the ending circle.
													endRadius:27]; // The radius of the ending circle.
```

###Use gradient pattern image as Forgeground color on icon

```objective-c
	NSArray *githubColors = @[(id)[UIColor colorWithWhite:0.2 alpha:1.0].CGColor,
						   (id)[UIColor colorWithWhite:0.1 alpha:1.0].CGColor,
						   (id)[UIColor colorWithWhite:0.35 alpha:1.0].CGColor];
	NSArray *githubLocations = @[@0.2, @0.5, @1.0];
	UIImage *githubGradientPattern = [FontAwesomeKit linearGradientImageWithSize:CGSizeMake(45, 45)
																		  colors:githubColors
																	   locations:githubLocations];
	NSDictionary *githubAttr =@{FAKImageAttributeForegroundColor:[UIColor whiteColor],
							 FAKImageAttributeBackgroundColor:[UIColor colorWithPatternImage:githubGradientPattern]};
	self.gradientImageView.image = [FontAwesomeKit imageForIcon:FAKIconGithub
													  imageSize:CGSizeMake(45, 45)
													   fontSize:45
													 attributes:githubAttr];
```

**Available attributes:** (Both are optional, use default value if you don't specify)

######FAKImageAttributeRect
The value of this attribute is a NSValue object containing a CGRect structure. You can wrap a CGRect structure into NSValue object like this:
`NSValue *rectValue = [NSValue valueWithCGRect:aCGRect];`  
*Default: Center the icon in both directions.*
  
######FAKImageAttributeForegroundColor
The value of this attribute is an UIColor object. Use this attribute to specify the color of the icon.
*Default: Black color.*

######FAKImageAttributeBackgroundColor
The value of this attribute is an UIColor object. Use this attribute to specify the color of the background area behind the icon.  
*Default: Transparent color.*


######FAKImageAttributeFont
The value of this attribute is an UIFont object. Use this attribute to specify the icon font you want to use. You can pass the value to use another icon font.  
*Default: Use FontAwesome*
