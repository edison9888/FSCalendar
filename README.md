
![fscalendar](https://cloud.githubusercontent.com/assets/5186464/6655324/213a814a-cb36-11e4-9add-f80515a83291.png)<br/><br/>
[![Version](https://img.shields.io/cocoapods/v/FSCalendar.svg?style=flat)](http://cocoadocs.org/docsets/FSCalendar)
[![License](https://img.shields.io/cocoapods/l/FSCalendar.svg?style=flat)](http://cocoadocs.org/docsets/FSCalendar)
[![Platform](https://img.shields.io/cocoapods/p/FSCalendar.svg?style=flat)](http://cocoadocs.org/docsets/FSCalendar)

## Example
![fscalendar1](https://cloud.githubusercontent.com/assets/5186464/6652191/f11d5242-caa1-11e4-9cc2-8a7c0cc9ef02.gif)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
![fscalendar2](https://cloud.githubusercontent.com/assets/5186464/6652193/19e7f92a-caa2-11e4-92af-0639dc0c2d79.gif)

## Installation

* Using cocoapods:`pod 'FSCalendar'` 
* Manually: Drag all .h and .m files in FSCalendar group to your project

```objective-c
#import "FSCalendar.h"
```

## Setup

### Use Interface Builder (Recommended)

1. Drag two UIView objects to ViewController Scene, change the `Custom Class` to `FSCalendarHeader` and `FSCalendar`<br/>
![fscalendar-storyboard1](https://cloud.githubusercontent.com/assets/5186464/6655136/a3cc77b4-cb2a-11e4-8dc2-886e61d2abdb.png) <br />
![fscalendar-storyboard2](https://cloud.githubusercontent.com/assets/5186464/6655137/a86c1bb2-cb2a-11e4-9a0d-15b28a72e1eb.png)
<br/>
2. After adjust the position and frame, link `header` property of the calendar to the header, and the `dataSource` and `delegate` to the ViewController <br/>
![fscalendar-storyboard3](https://cloud.githubusercontent.com/assets/5186464/6655159/ac02925a-cb2b-11e4-885e-a287ad5c7769.png)
3. Implement `FSCalendarDataSource` and `FSCalendarDelegate` in ViewController.m

### Use code

In viewDidLoad (or loadView) of ViewController.m
```objective-c
FSCalendarHeader *header = [[FSCalendarHeader alloc] initWithFrame:CGRectMake(0, 0, 320, 44)];
[self.view addSubview:header];
FSCalendar *calendar = [[FSCalendar alloc] initWithFrame:CGRectMake(0, 44, 320, 280)];
calendar.header = header;
calendar.dataSource = self;
calendar.delegate = self;
[self.view addSubview:calendar];
self.calendar = calendar;
```

## Core classes

### FSCalendar

```objective-c
@property (weak, nonatomic) IBOutlet id<FSCalendarDelegate> delegate;
```
A delegate object to handle common user tap/scroll event, see `FSCalendarDelegate` for details.

```objective-c
@property (weak, nonatomic) IBOutlet id<FSCalendarDataSource> dataSource;
```
A dataSource object to provide subtitle, event dot or other sources, see `FSCalendarDataSource` for details.

```objective-c
@property (weak, nonatomic) IBOutlet FSCalendarHeader *header;
```
An UIView subclass which afford a scrolling effect for month symbol.

```objective-c
@property (assign, nonatomic) FSCalendarFlow flow;
```
An enumeration value to determine the scroll direction of `FSCalendar`, default value is `FSCalendarFlowHorizontal`

```objective-c
@property (assign, nonatomic) BOOL autoAdjustTitleSize;
```
The text size of `FSCalendar` is automaticly calculated based on the frame by default. To turn it off, set this value to `NO`.

```objective-c
@property (copy, nonatomic) NSDate *currentDate;
```
The current date of calendar, default is [NSDate date];

```objective-c
@property (readonly, nonatomic) NSDate *selectedDate;
```
Get the selected date of `FSCalendar`

```objective-c
@property (readonly, nonatomic) NSDate *currentMonth;
```
Get the current month of `FSCalendar`.Extract it with `NSDateComponents`, or `currentMonth.fs_month` and `currentMonth.fs_year`

```objective-c
@property (assign, nonatomic) FSCalendarCellStyle cellStyle UI_APPEARANCE_SELECTOR;
```
The background style for `today` and `selected cell`, default is FSCalendarCellStyleCircle.

```objective-c
@property (strong, nonatomic) UIFont   *titleFont UI_APPEARANCE_SELECTOR;
```
The font for `day` text. To change the font size, set `autoAdjustTitleSize` to `NO`

```objective-c
@property (strong, nonatomic) UIFont   *subtitleFont UI_APPEARANCE_SELECTOR;
```
The font for `subtitle` text. To change the font size, set `autoAdjustTitleSize` to `NO`

```objective-c
@property (strong, nonatomic) UIFont   *weekdayFont UI_APPEARANCE_SELECTOR;
```
The font for `weekday` text. To change the font size, set `autoAdjustTitleSize` to `NO`

```objective-c
@property (strong, nonatomic) UIFont   *headerTitleFont UI_APPEARANCE_SELECTOR;
```
The font for scrolling header text. To change the font size, set `autoAdjustTitleSize` to `NO`

```objective-c
@property (strong, nonatomic) UIColor  *eventColor UI_APPEARANCE_SELECTOR;
```
The color for event dot.

```objective-c
@property (strong, nonatomic) UIColor  *weekdayTextColor UI_APPEARANCE_SELECTOR;
```
The text color of weekday. 

```objective-c
@property (nonatomic) UIColor *titleDefaultColor UI_APPEARANCE_SELECTOR;
```
The `day text color` for default state.

```objective-c
@property (nonatomic) UIColor *titleSelectionColor UI_APPEARANCE_SELECTOR;
```
The `day text color` for selection state.

```objective-c
@property (nonatomic) UIColor *titleTodayColor UI_APPEARANCE_SELECTOR;
```
The `day text color` where the date is equal to `currentDate`.

```objective-c
@property (nonatomic) UIColor *titlePlaceholderColor UI_APPEARANCE_SELECTOR;
```
The `day text color` where the date is `not` in `currentMonth`.

```objective-c
@property (nonatomic) UIColor *titleWeekendColor UI_APPEARANCE_SELECTOR;
```
The `day text color` where the date is weekend.

```objective-c
@property (nonatomic) UIColor *subtitleDefaultColor UI_APPEARANCE_SELECTOR;
```
The `subtitle text color` for default state.

```objective-c
@property (nonatomic) UIColor *subtitleSelectionColor UI_APPEARANCE_SELECTOR;
```
The `subtitle text color` for selection state.

```objective-c
@property (nonatomic) UIColor *subtitleTodayColor UI_APPEARANCE_SELECTOR;
```
The `subtitle text color` where the date is equal to `currentDate`.

```objective-c
@property (nonatomic) UIColor *subtitlePlaceholderColor UI_APPEARANCE_SELECTOR;
```
The `subtitle text color` where the date is `not` in `currentMonth`.

```objective-c
@property (nonatomic) UIColor *subtitleWeekendColor UI_APPEARANCE_SELECTOR;
```
The `subtitle text color` where the date is weekend.

```objective-c
@property (nonatomic) UIColor *selectionColor UI_APPEARANCE_SELECTOR;
```
The `cell background color` for selection state.

```objective-c
@property (nonatomic) UIColor *todayColor UI_APPEARANCE_SELECTOR;
```
The `cell background color` where the date is equal to `currentDate`.

```objective-c
@property (nonatomic) UIColor  *headerTitleColor UI_APPEARANCE_SELECTOR;
```
The `text color` for `FSCalendarHeader`.

```objective-c
@property (nonatomic) NSString *headerDateFormat UI_APPEARANCE_SELECTOR;
```
The `date format` for `FSCalendarHeader`.

#### FSCalendarDataSource

```objective-c
- (NSString *)calendar:(FSCalendar *)calendar subtitleForDate:(NSDate *)date;
```
To provide a subtitle right below the `day` digit. 

```objective-c
- (BOOL)calendar:(FSCalendar *)calendar hasEventForDate:(NSDate *)date;
```
To provide an event dot below the day cell.

#### FSCalendarDelegate

```objective-c
- (BOOL)calendar:(FSCalendar *)calendar shouldSelectDate:(NSDate *)date;
```
To determine whether the day cell should be selected and show the selection layer.

```objective-c
- (void)calendar:(FSCalendar *)calendar didSelectDate:(NSDate *)date;
```
This method would execute after a cell is managed to be selected and show the selection layer. 

```objective-c
- (void)calendarCurrentMonthDidChange:(FSCalendar *)calendar;
```
This method would execute when calendar month page is changed. 

## Requirements
ios 7.0

## Known issues
1. The title size changed as we change frame size of FSCalendar: Automatically adjusting font size based on frame size is default behavior of FSCalendadr, to disable it:

```objective-c    
self.calendar.autoAdjustTitleSize = NO; 
self.calendar.titleFont = otherTitleFont;
self.calendar.subtitleFont = otherSubtitleFont;
```

`titleFont` and `subtitleFont` is also available for `UIAppearance` selector, but would not take any effect if `autoAdjustTitleSize` value is `YES`

## Author

Wenchao Ding, f33chobits@gmail.com

## License

FSCalendar is available under the MIT license. See the LICENSE file for more info.

## Others
* If FSCalendar cannot meet your requirment, welcome to submit issues or pull request
* If you are using this library and using custom color modulation, please take a screenshot for your calendar appearance [here](https://github.com/f33chobits/FSCalendar/issues/2), this will help others better matching color in their apps, thanks
