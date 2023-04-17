# Gray Area Festival Video Archive

https://quilime.github.io/gray-area-video-archive


## TODO

### Aggregation Page

  - [ ] Festival description per year
  - [ ] Hot tags
  - [x] Starting page
  - [x] Rev chron by year (sortable)
  - [x] Year tags

### Logo Bumper for New Videos

  ### 2021 - Worlding
  - [ ] Add Logo Bumper to Each Video
  - [ ] Re-upload each video.

  ### 2022 - Distant Early
  - [ ] Add Logo Bumper to Each Video
  - [ ] Re-upload each video
  - [ ] Presenter Name


## New Metadata

  - Used for more fidelity in Video Archive
  - Retrieved in Video JSON and parsed
  - Metadata delimiter (6 equals signs) "======"
  - `key: value` format
  - Append raw metadata to bottom of YouTube Description field
  - When parsed in the archive JSON, prepended with `meta_`, for example, `festival_year: 2015` becomes `{ "meta_festival_year" : "2015" }` in the archive json

```
======
featured: <featured person(s), or group>
featured_url: https://www.ruhabenjamin.com
festival_year: 2015
... additional metadata as needed ...
```

## Scripts


## Compile Archive Database

Compile JSON formatted database to be queried from the front end.

Usage `compile-db.js source dest`

- `source` A JSON file or folder of JSON files of YouTube metadata scraped from YouTube via ytdlp
- `dest` A destination folder to write the JSON single-file database. Will prompt to confirm overwrite.


## Get YouTube Metadata

Download YouTube metadata in JSON format from single YouTube video, playlist, or playlists.

Usage `get-youtube-metadata.sh destination`

- `destination` A destination folder to save the JSON data

Examples
```
# 2021
./bin/get-youtube-metadata.sh https://www.youtube.com/playlist?list=PLm8zJ0HKEJIb5NO3fjqIb7o2AxxIqU2w- ./data/videos/2021/

# 2020
./bin/get-youtube-metadata.sh https://www.youtube.com/playlist?list=PLm8zJ0HKEJIaarwTpOzGg4DXXVLWy2GVU ./data/videos/2020/

# 2019
./bin/get-youtube-metadata.sh https://www.youtube.com/playlist?list=PLm8zJ0HKEJIZXGbpAdjpIP9cuuJYfOW-F ./data/videos/2019/

# 2018
./bin/get-youtube-metadata.sh https://www.youtube.com/playlist?list=PLm8zJ0HKEJIaNfzV_-f0aYvrpAZAzjhIl ./data/videos/2018/

# 2017
./bin/get-youtube-metadata.sh https://www.youtube.com/playlist?list=PLm8zJ0HKEJIYAk9rAz1CQmE9Pzn8G_hrq ./data/videos/2017/

# 2016
./bin/get-youtube-metadata.sh https://www.youtube.com/playlist?list=PLm8zJ0HKEJIZtQ0PqjW341QIWrqPPkQXi ./data/videos/2016/

# 2015
./bin/get-youtube-metadata.sh https://www.youtube.com/playlist?list=PLm8zJ0HKEJIZz_vKS1amJguyAEIiTtxjw ./data/videos/2015/
```

## Get YouTube Subs from Json Data

Download YouTube auto-generated subtitles in English (en) .vtt subtitle format using information existing YouTube JSON metadata (prerequiste). Will create .vtt files alongside source JSON

Usage `get-all-subs.sh sourceDir`

- `sourceDir` A source folder of YouTube JSON metadata files


## Get YouTube Autogenerated Transcription/Subtitles

Download auto-generated transcription/subtitles in English for given YouTube ID

Usage `get-youtube-subs.sh youtube_id [dest]`

- `youtube_id` A YouTubeID
- `dest` (optional) .vtt output destination. Default output will be alongside the source.


## Localhost (dev)

Serve locally for dev via Python http server

Usage: `serve`


# Notes

alpine and pagination
https://www.raymondcamden.com/2022/05/02/building-table-sorting-and-pagination-in-alpinejs
https://codepen.io/cfjedimaster/pen/ExQaZQZ

openai whisper
https://www.pinecone.io/learn/openai-whisper/
https://www.youtube.com/watch?v=vpU_6x3jowg
https://github.com/jamescalam/ask-youtube/tree/main/youtube-search

subtitles
https://superuser.com/questions/927523/how-to-download-only-subtitles-of-videos-using-youtube-dl

download subs for id
yt-dlp --sub-lan=en --write-auto-sub --skip-download vy2yuh_ENNA


only list selected keys

    <div x-data="{ open: false, selectedKeys: ['id', 'title', 'description', 'duration', 'playlists'] }">
      <h3><a href="#;" x-on:click="open = !open" x-text="'Metadata ' + (open ? '▾' : '▸')"></a></h3>
      <template x-if="open">
        <ul>
          <template x-for="key in Object.keys(selVideo).filter(key => selectedKeys.includes(key))">
              <li>
                <span x-text="key"></span>
                <span x-html="String(selVideo[key]).replace(/\n/g, '<br />')"></span>
              </li>
          </template>
        </ul>
      </template>
    </div>