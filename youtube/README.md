# Personal Youtube userstyle

This style provides adjustable video columns, compact watch history, and theater mode that fills the page height.

## Installation and configuration

1. Install [Stylus for Firefox](https://addons.mozilla.org/firefox/addon/styl-us/)
2. The [YouTube installation link](https://raw.githubusercontent.com/dnery/usercss/main/youtube/youtube.user.css) (raw contents of the file) opens the Stylus installer
3. Select **Install style**, or **Update style** for an existing installation
4. On YouTube, open the Stylus popup and configure the parameters

The configuration controls apply changes without a source edit:

| Control               | Default     | Available values                        |
| --------------------- | ----------- | --------------------------------------- |
| Videos per row        | 4           | 3 to 6                                  |
| History Shorts width  | 120 px      | 90 to 180 px                            |
| History sidebar width | 240 px      | 200 to 320 px                           |
| Theater video fit     | Whole video | Whole video or Fill player (crop edges) |

The column count also controls the width of loading cards. The history sidebar scrolls with the page. When the history content area is 900 px wide or less, its controls move above the video list.

Theater mode fills the visible page below the YouTube header. Scroll down to see the details, comments, and suggestions. The default **Whole video** mode preserves the video proportions and can leave bars when the player and video proportions differ. **Fill player (crop edges)** removes those bars through cropping. Neither mode stretches the image.

The style hides browse-page Shorts shelves, watch-page Shorts suggestions, notification and creation buttons, voice search, and text under compact guide icons. History Shorts remain visible. The style keeps the normal player layout and fullscreen sizing under YouTube control.

## Local changes

From the repository directory, start a local HTTP server:

```sh
python3 -m http.server 8769 --bind 127.0.0.1
```

1. Open <http://127.0.0.1:8769/youtube.user.css> in Firefox.
2. Install or update the style through Stylus.
3. Enable **Live reload after installation** if you want Stylus to apply file changes during development.
4. After the layout checks, stop the server with Ctrl+C.

The `@updateURL` points to GitHub, even when installation uses the local server. The server is necessary only for local installation or live reload. Keep the disabled old style until you are satisfied with the replacement.

## Publishing and updates

Stylus can update each style independently from one repository. Each file has its own metadata, version, configuration, and raw URL. GitHub Pages, releases, and a listing on a style website are optional.

For example, two files in a repository named `userstyles` can use these update URLs:

```text
https://raw.githubusercontent.com/dnery/userstyles/main/youtube.user.css
https://raw.githubusercontent.com/dnery/userstyles/main/another-site.user.css
```

To publish a change:

1. Make sure that the style passes the layout checks in Firefox.
2. Increase `@version` in the changed file, for example from `0.4.0` to `0.4.1`.
3. Commit and push the file to the branch in its `@updateURL`.
4. Use **Check for update** in Stylus to request the new version.

Stylus also checks for updates automatically when updates are enabled. Keep `@name`, `@namespace`, and variable keys stable across updates. Stylus preserves saved configuration values when the corresponding variable keys remain available.

After a repository rename, update `@homepageURL`, `@updateURL`, and the installation links. Increase the style version with that change. If the old URL stops serving the file, install from the new raw URL to restore updates. Do not depend on redirects as a permanent update path.

See the [Stylus UserCSS documentation](https://github.com/openstyles/stylus/wiki/Writing-UserCSS) for metadata and update behavior.

## Layout checks

Version `0.4.0` passed these checks in the current Firefox session on November 3, 2026:

- Video rows contain 3, 4, 5, or 6 cards, as selected.
- Continuation loading cards match the video card width at each column count.
- History uses a 240 px sidebar and 120 px Shorts cards without horizontal page overflow.
- An 800 px history content area puts the controls above the list.
- Theater mode fills the height below the 56 px header with Sidebery open and closed.
- Whole-video and crop-to-fill values apply to the theater player.
- The normal player and fullscreen remain usable, and comments remain reachable through scrolling.

YouTube can change its HTML structure without notice. New page variants and future browser versions require another layout check. The initial page-loading skeleton has CSS coverage, but the live measurements covered continuation loading cards.
