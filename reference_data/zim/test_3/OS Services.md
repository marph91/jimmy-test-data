The operating provides various generic services to the app containers via **os-services**
Each image spec states which services the app wants to use, on deployment these are
configured for runtime use.

- [ ] x11
    * access to an X11 based display server for presenting the GUI.
    * in simple cases it's the host user's X server
    * might well be an isolated instance
    * app may not take any specific assumptions on the X environment (WM, etc)
- [ ] temp-homedir
    * provides app-writable home directory under /home/app
    * deleted as soon as the app container terminates
    * app may take no assumptions of available space
- [ ] user-pictures
    * a plain directory with the user's picture collections
    * may have subdirectories
    * permissions:
        * list files
        * read files
        * (over)write files
        * create new files
- [ ] user-documents
    * a plain directory with the user's documents
    * may have subdirectories
    * permissions:
        * list files
        * read files
        * (over)write files
        * create new files
        * dummy-write (writes to separate tmpfs layer)
- [ ] settings-dir:
    * a plain app-writable directory for storing application settings
    * only meant for low volume data, mostly-read
    * included in app backups
    * mounted at [/home/app/settings](settings)
- [ ] cache-dir:
    * a plain app-writable directory for cache data
    * may grow as large as system (or runtime) allows
    * user may impose arbitrary restrictions at will
    * may be removed by the host at will (either completely or individual files)
    * if app uses system-notification service, it gets notification on cache purge

Planned (not yet implemented) services:

- [ ] factotum:
    * credential management via Plan9's factotum server
- [ ] cache-dir
    * auto-maintenance settings (eg. different TTLs per subdir)
- [ ] user-pictures-thumbs:
    * automatic/on-demand thumbnail generation (and cache purging)
- [ ] audio playback
    * directly play audio files (given via FD)
    * play system sounds (given by name)
    * permissions
        * allowed-always
        * allowed-focus (when app has focus)
        * take-focus (make silence others temporarily, eg. phone ring)
- [ ] video playback
    * play various video streams/files in a given GL surface
- [ ] system notification
    * notifies the app on certain events:
        * cache purge
        * resource pressure
        * system / UI idle (eg for doing background jobs)
        * powersave (eg when apps shall only do essential things)
    * may be user-controlled per app, thus apps cant rely on getting notifies
    * may be synthetic, means: individual apps shall behave like in certain situation (eg. sleep in order to free resources for other jobs)
    * graceful restart (on update)
        * app can do temporary quick save or store open fds to pick them up after restart
- [ ] environment change
     * user can define different environments where app can behave differently
    * e.g. stationary vs mobile, light conditions, etc
    * 2do: standardize naming / schema for common cases
