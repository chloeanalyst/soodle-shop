# soodle-shop

The live shop catalogue for the Soodle app. The app downloads `shop.json` from
https://chloeanalyst.github.io/soodle-shop/shop.json each time it opens, so anything changed here
reaches everyone without an app update (usually within a few minutes of saving).

If the file is broken or can't be reached, the app keeps using the last good copy, or the one built into it.

## What's in shop.json

| Part | What it does |
|---|---|
| `version` | Raise it by 1 every time you change the file. It must never be lower than the number built into the app. |
| `events` | Double-hearts weekends and the like, with start and end dates (`"2026-11-28"`, whole days count). |
| `banners` | The swiping banners at the top of the shop. |
| `collections` | Sets sold together at a discount (`theme`: `autumn`, `winter` or `none`). |
| `sales` | Items on sale for a while, with an optional countdown. |
| `newIds` | Items marked "New". |
| `hiddenIds` | Items taken off the shelves for now. |
| `newItems` | Brand-new items that aren't built into the app (see below). |

Items are written as `"category:number"`, for example `"jumper:12"` or `"bed:20"`.

## Adding a brand-new item

Works for jumpers, bandanas, necklaces and sunglasses.

1. Give it the next number after the ones in the app: jumpers from 21, bandanas from 28, necklaces from 43,
   sunglasses from 9.
2. Put its pictures (PNG, same sizes as the built-in ones) in the `items` folder, named exactly like this
   (for jumper 21):

   | Category | Pictures |
   |---|---|
   | jumper | `jumper_tile_21.png`, `jumper_worn_21.png`, `dog_jumper_21.png`, `dog_jumper_neck_21.png` |
   | bandana | `bandana_tile_N.png`, `bandana_worn_N.png`, `dog_bandana_N.png` |
   | necklace | `necklace_tile_N.png`, `necklace_worn_N.png`, `dog_necklace_N.png` |
   | glasses | `glasses_tile_N.png`, `dog_glasses_N.png` |

3. Add it to `newItems`:

   ```json
   "newItems": [
     { "category": "jumper", "k": 21, "name": "Pumpkin stripe", "hearts": 64 }
   ]
   ```

4. Optionally add `"jumper:21"` to `newIds` so it shows as New.

The item only appears in the app once every one of its pictures has downloaded, so a missing picture never shows
a broken item.
