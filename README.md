# chore-tinder-objc

An Objective-C based iOS application for assigning people to Chores on a weekly basis.

![Chore Tinder Objc](https://i.imgur.com/8Drc9CS.jpg)

## Description

A ridiculously simple, stock standard iOS application for assigning people to chores on a weekly basis. Built as an exercise in writing Objective C for a mobile application that interacts with common Foundation and UIKit APIs such as `UITableView`, `NSURLSession`, `NSURLSessionDataTask`, `NSCalendar`, `Grand Central Dispatch (GCD)`, `UIAlertController`, `NSError` and `NSJSONSerialization`. Not intended to be useful in any way, or be architecturally interesting, instead exists as an excercise in becoming familiar again with programming in Objective C as opposed to that other language that shall henceforth not be named.

It integrates with a hacky little [NodeJS API that I wrote](https://github.com/phillfarrugia/chore-tinder-api) to store the schedules in a MongoDB database. Think of it what you will, the purpose here was to have some fun and write some Objective C not to do anything worth writing home about.

## Features

### Weekly Schedules

Displays the schedule for the current calendar week on run. Navigate between the schedule for each week of the year by tapping Previous, Next.

### Assign Chores

People are assigned to chores by tapping on the desired day and typing their name into the `UIAlertViewController's` text field.

## Architecture

![Architecture](https://i.imgur.com/peN2EPt.png)

### ScheduleViewController
Since this application is such a simple application with very limited functionality, it's current architecture reflects its limitations. Upon loading `ScheduleViewController` requests Data about its current Schedule from its `ScheduleDataSource`. This object exists in order to abstract away any data-specific logic from the ViewController layer, which is not specifically relevant to the User Interface. No business logic is implemented on the View Controller, it exists simply to coordinate the DataSource and the Views.

### ScheduleDataSource
The DataSource handles keeping track of the current Schedule, and its identifier, as well as building an `NSURLRequest` to be sent to its underlying to the `HTTPCommunicator`.

### HTTPCommunicator
A stateless class that wraps around and coordinates with Foundation's `NSURLSession` and `NSURLSessionDataTask`. Asynchronous tasks are sent and upon completion any errors are handled and the response data is passed back to the calling DataSource via a block parameter or completion handler.

### DayOfWeekTableViewCell
A `UITableViewCell` who's sole purpose is to take configure itself with a `day` string and an `assignee` string, by presenting them with two `UILabels`.

## Frequently Asked Questions

### Why is this such a plain, ridiculously simple project?

I built this in a couple of hours on a weekend, in order to give myself an excuse to write some Objective C. I've opened sourced it, because why not? And might in the future pick it back up and develop it into something more interesting and more architecturally valuable in the future but for now it is what it is.

### Why is it called Chore Tinder?

It's just an iOS implementation of a Slack bot that an old colleague wrote which allowed team members to be assigned to office chores which went by the same name.

## Contributions

I have no immediate plans to actively work on this experiment any further. However this source code is licensed under the [MIT license](https://github.com/phillfarrugia/swipeable-view-stack/blob/master/LICENSE) which permits anyone to fork this repository and make modifications under the same license.
