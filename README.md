# Apple Music Recommendation & Queue Shortcut

This Shortcut integrates with Apple Music to:

1. Get the currently playing song in the Music app
2. Fetch track recommendations from the Better Radio API
3. Queue recommended tracks in your Up Next list

**Shortcut Link:** [Add to Shortcuts](https://www.icloud.com/shortcuts/5e3e4d50caf24910aa871207fae0cb7d)

## Prerequisites

* A Mac or iOS device running **macOS Monterey** (12.0) or later / **iOS 15** or later
* The **Shortcuts** app installed
* Access to the Apple Music app with an active subscription
* Internet connectivity to call the API endpoint

## Installation

1. Click the **Add to Shortcuts** link above.
2. The Shortcuts app will open and prompt you to add the Shortcut to your library.
3. Optionally, rename the Shortcut (e.g. **Better Radio Queue**). Ensure all internal variables remain unchanged.

## Usage

1. Open Apple Music and start playing any song.
2. Run the **Better Radio Queue** Shortcut from the Shortcuts app, Dock, or via Siri:

   > "Hey Siri, run Better Radio Queue"
3. Watch the Quick Look (or Show Result) action display the queued tracks, or open the Up Next queue in Music to see them.

## Shortcut Workflow

1. **Get Current Song**
   Retrieves the track currently playing in Apple Music.

2. **Extract Details**

   * **Name** → stores in `SongName`
   * **Artist** → stores in `ArtistName`

3. **URL‑Encode Parameters**

   * Encodes `SongName` → `EncodedSong`
   * Encodes `ArtistName` → `EncodedArtist`

4. **Build Request URL**
   Constructs:

   ```
   https://api-better-radio-1085889685327.asia-south1.run.app/recommend/track?song_name=[[EncodedSong]]&artist_name=[[EncodedArtist]]
   ```

5. **Get Contents of URL**
   Calls the Better Radio API and parses JSON response into a dictionary.

6. **Extract `song_names`**
   Retrieves the array of recommended track names into `RecommendedSongs`.

7. **Repeat Loop**
   For each item in `RecommendedSongs`:

   1. **Find Music Where Name is Repeat Item**
      Searches the Apple Music library for a matching track (limit 1).
   2. **Add Music to Up Next**
      Queues the found track in the Up Next list.


## Troubleshooting

* **Blank or Missing Recommendations**
  • Ensure your device is online.
  • Verify the Shortcut’s URL uses the correct API endpoint.
  • Test with a known song (e.g. by inserting a Text action as mock input).

* **Variable Errors**
  • On macOS, rename variables by ⌃‑clicking the blue pill or by using a **Set Variable** block.

* **No Track Found**
  • The exact metadata in your library may differ. Check spelling or try a manual search first.

## Customization

* **Change Recommendation Source**
  • In the **Text** action building the URL, replace the base URL with any compatible API.

* **Adjust Queue Behavior**
  • Instead of **Up Next**, use **Play Music**, **Add to Playlist**, or other Music actions.

---
