# [fit] _CocoaPods_ Dependency Resolution:
# [fit] Introducing _**Molinillo**_
<br>
## Samuel E. Giddins
## @_segiddins_

^ I'm a core team member
^ Doing this instead of being a triple major at UChicago for a year

---

![](image/cocoapods-white-on-orange.jpg)

^ The ObjC package manager.
^ 100,000s of users building the best iOS and Mac apps
^ Important b/c it allows the community to share code and focus on whatever it is they do best

---

# Releases
## [fit] 0.34.0.rc1, 0.34.0, 0.34.1, 0.34.2, 0.34.4

^ Special thanks to Fabio, Alloy and Kyle and the rest of the Core team for making these releases possible (and doing most of the hard work)

---

# _**Molinillo**_
## [fit] Dependency Resolution Gem

![left](image/mexican-molinillo.jpg)

---

### But first, a detour

---

## The *Podspec*

```ruby
Pod::Spec.new do |s|
  s.name     = 'PromiseKit-AFNetworking'
  s.version  = '0.1.4' 
  s.dependency 'AFNetworking', '~> 2.0'
  s.dependency 'PromiseKit/Promise'
end
```

---

## The *Podfile*

```
source 'https://github.com/CocoaPods/Specs'
platform, :ios, '8.1'
pod 'AFNetworking', '< 1.3'
pod 'RestKit', '~> 0.23.0'
pod 'SEGModules', git: 'https://github.com/segiddins/SEGModules.git'
```

^ Specifies explicit dependencies
^ Different types of requirements, including external sources

---

### How it Works

---

### Encapsulation

- SpecificationProvider
- UI

^ SP translates client-side domain knowledge into answers for Molinillo
^ UI prints out pretty dots every second

---

### The Algorithm

- Constrainst Solving Problem
- Backtracking
- Forward Checking

^ forward checking = stop as soon as you hit a dead end (dont color in the rest of the picture)
^ Hard CSP because the sets of constraints are dynamic -> no easy graph theory answer 😞

---

### Stack of __States__
### And :loop:

---

### Sort Dependencies
### Handle One
### Create a Possibility State

---

### See if it works

---

### Yes *=>* move on
### No *=>* unwind for conflict

---

### [fit] Stop when all requirements are activated

---

### [fit] Raise when there are no possibible states left

---

## Examples

---

```
platform :ios, "7.0"
inhibit_all_warnings!
pod 'RestKit'
pod 'AFNetworking', '~> 1.2.0'
```

Before:

```
[!] Unable to satisfy the following requirements:

- `AFNetworking (~> 1.3.0)` required by `RestKit/Network (0.23.3)`
- `AFNetworking (~> 1.2.0)` required by `Podfile`
```

---

```ruby
platform :ios, "7.0"
inhibit_all_warnings!
pod 'RestKit'
pod 'AFAmazonS3Client'
pod 'CargoBay'
pod 'AFOAuth2Client'
```
Before:

```
[!] Unable to satisfy the following requirements:

- `AFNetworking (~> 1.3.0)` required by `RestKit/Network (0.23.3)`
- `AFNetworking (~> 1.2.0)` required by `Podfile`
```

---

```ruby
platform :ios, "7.0"
inhibit_all_warnings!
pod 'AFAmazonS3Client'
pod 'CargoBay'
pod 'AFOAuth2Client'
```

Before: 

```
[!] Unable to satisfy the following requirements:

- `AFNetworking (~> 2.0)` required by `AFAmazonS3Client (2.0.0)`
- `AFNetworking/Serialization` required by `AFNetworking (2.4.1)`
- `AFNetworking/Security` required by `AFNetworking (2.4.1)`
- `AFNetworking/Reachability` required by `AFNetworking (2.4.1)`
- `AFNetworking/NSURLConnection` required by `AFNetworking (2.4.1)`
- `AFNetworking/NSURLSession` required by `AFNetworking (2.4.1)`
- `AFNetworking/UIKit` required by `AFNetworking (2.4.1)`
- `AFNetworking/Serialization` required by `AFNetworking/NSURLConnection (2.4.1)`
- `AFNetworking/Reachability` required by `AFNetworking/NSURLConnection (2.4.1)`
- `AFNetworking/Security` required by `AFNetworking/NSURLConnection (2.4.1)`
- `AFNetworking/Serialization` required by `AFNetworking/NSURLSession (2.4.1)`
- `AFNetworking/Reachability` required by `AFNetworking/NSURLSession (2.4.1)`
- `AFNetworking/Security` required by `AFNetworking/NSURLSession (2.4.1)`
- `AFNetworking/NSURLConnection` required by `AFNetworking/UIKit (2.4.1)`
- `AFNetworking/NSURLSession` required by `AFNetworking/UIKit (2.4.1)`
- `AFNetworking (~> 2.2)` required by `CargoBay (2.1.0)`
- `AFNetworking (~> 1.3)` required by `AFOAuth2Client (0.1.2)`
```

---

### __After:__

it *just works* :grinning:

^ This means we can let computers do what they're best at
^ Less need for manual intervention

---

# :cocktail: Stripe :cocktail:
# _:heart:_

---

## [fit] Samuel E. Giddins
### _CocoaPods_ Core Team
### @_segiddins_
