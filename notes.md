# TODO list schema:

search for which item to increment/check-off
items (and lists) age when they haven't been checked (how long before aging? maybe 1 week? 2 days?)
support Undo (which actually deletes the entry because we don't want logs of it maybe?)

types of things to have in a checklist:

- counters
  - simple check
  - calorie count
  - input prompt
- simple checklist
- LRU restaurants


# CheckList Fields

- id
- title: "Grocery List"
- sortedItemIds: []        (when a list needs to be sorted)
- orderBy:
- isDescending: false
- resetPeriod: day/24hrs/week/month/none (maybe this should be a list setting? prolly both places because dashboard has different metrics)


# CheckList Item Fields

- title: "Do Laundry"
- listId:
- createdAt:
- isVisible:
- type: 'simple|multicheck'

(additional fields for the multicheck option)

- defaultAmount
- unitName (dollars, minutes, calories, miles)


# CheckList ItemEntry Fields

- listItemId: (link to the entries)
- type: bool|number
- createdAt: 
- value: true|number
- GPSCoordinates: null


# Examples

## Count Calories

(sort these manually but show the running total for the day/week/month)

- listId: 'desktop counters'
- title: 'food'
- createdAt: 1/1/16
- type: 'multicheck'
- defaultAmount: 100
- unitName: 'Cal'
- resetPeriod: day/24hrs/week/month/none (maybe this should be a list setting? prolly not because dashboard has different metrics)
- ItemEntry: (link)
  - createdAt: 1/1/16
  - isVisible: true
  - type: 'number'
  - value: 150


# LRU Restaurants

(sort these by ItemEntry createdAt so the least-recently-visited ones show up on top)

- listId: 'restaurants'
- title: 'Pok Pok'
- createdAt: 1/1/16
- type: 'multicheck'
- defaultAmount: null
- unitName: null
- resetPeriod: 'year'
- ItemEntry: (link)
  - createdAt: 1/1/16
  - isVisible: true
  - type: 'number'
  - value: 1


## Count time spent Redditing

- listId: 'desktop counters'
- title: 'reddit'
- createdAt: 1/1/16
- type: 'multicheck'
- defaultAmount: 10
- unitName: 'min'
- isTimer: true              (sets a time that ticks down and then beeps but has a +1)
- resetPeriod: '24hrs'
- ItemEntry: (link)
  - createdAt: 1/1/16
  - isVisible: true
  - type: 'number'
  - value: 10

# Vanilla Checklist

- listId: 'groceries'
- title: 'Onions'
- createdAt: 1/1/16
- type: 'simple'        (maybe the type should be on the list, not the item?)
- defaultAmount: null
- unitName: null
- resetPeriod: 'none'   (maybe the resetPeriod should be on the list? and the item can override?)
- ItemEntry: (link)
  - createdAt: 1/1/16
  - isVisible: true
  - type: 'boolean'
  - value: true





UI For the counter items:

```
+==================================================+
| Groceries                                        |
+==================================================+
| ( ) Onions                                       |
+--------------------------------------------------+
| (X) Milk                                         |
+--------------------------------------------------+
| ( ) Cheese                                       |
+--------------------------------------------------+



+==================================================+
| Daily Life                         (every 24hrs) |
+==================================================+
| [+100] Food                              325 Cal |
+--------------------------------------------------+
| [+0.5] Run                                1.3 mi |
+--------------------------------------------------+
| [+10 ] reddit (4min left)                 76 min |
+--------------------------------------------------+



+==================================================+
| Restaurant Picker                   (every year) |
+==================================================+
| [+1] PokPok                       (3 months ago) |
+--------------------------------------------------+
| [+1] Burgerville                  (2 months ago) |
+--------------------------------------------------+
| [+1] Bollywood                       (1 day ago) |
+--------------------------------------------------+

```
