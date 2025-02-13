# Automated Movie Collection Manager

A Python-based automation tool that helps manage movie collections by integrating TMDB, Real-Debrid, and Jellyfin. Search for movies by keywords, automatically send them to Real-Debrid, and organize them into Jellyfin collections.

## Features

- Search movies by keywords using TMDB API
- Automated torrent search across multiple sites (1337x, YTS, Nyaa)
- Smart torrent selection based on quality and seeder count
- Real-Debrid integration for secure downloading
- Automatic Jellyfin collection management
- Multi-threaded processing for faster operations
- Rate-limiting protection for API calls

## Prerequisites

- Python 3.x
- [Jellyfin](https://jellyfin.org/) server (plex/emby currently not supported)
- Real-Debrid account and api key
- TMDb account and api key
- [Zurg](https://github.com/debridmediamanager/zurg-testing) setup for Real-Debrid
- [Rclone](https://rclone.org) for cloud storage mounting in windows explorer

## Installation

1. Clone the repository:
```bash
git clone https://github.com/robinbtw/tmdb-automation.git
cd tmdb-automation
```

2. Install required packages:
```bash
pip install -r requirements.txt
```

3. Create a `.env` file in the root directory with your configuration:
```env
# Jellyfin Configuration
JELLYFIN_SERVER=http://your-server:8096
JELLYFIN_API_KEY=your-api-key
JELLYFIN_MOVIE_LIBRARY_ID=your-library-id

# TMDb Configuration
TMDB_API_KEY=your-tmdb-api-key
TMDB_API_URL=https://api.themoviedb.org/3

# Real-Debrid Configuration
REAL_DEBRID_API_KEY=your-real-debrid-api-key
```

## Usage

Run the script with command line arguments:

```bash
python main.py -k "keyword" -m max_results -w workers
```

Arguments:
- `-k, --keyword`: Search keyword (use quotes for multiple words)
- `-m, --max-results`: Maximum number of movies to process (default: 30)
- `-w, --workers`: Number of parallel workers (default: 1)

Example:
```bash
python main.py -k "action" # generic genre may be too vague
python ma1n.py -k "racing" # racing movies
python main.py -k "time travel" -m 20 # time travel movies (max 20 results)
python main.py -k "superhero" -m 50 -w 6 # superhero movies (max 50 results, 6 workers)
```

## Supported Torrent Sites
- 1337x
- YTS
- Nyaa

## Features Breakdown

### TMDB Integration
- Keyword-based movie search
- Movie details and metadata retrieval
- Smart movie filtering based on ratings

### Real-Debrid Features
- Multi-site torrent search
- Quality-based torrent selection (preferring 1080p/BluRay)
- Automatic magnet handling
- Cache checking to avoid duplicates

### Jellyfin Integration
- Automatic collection creation
- Smart movie matching
- Library scanning and updates
- Batch movie processing

## Notes
- The default worker count is set to 1 to avoid rate limiting
- Increase workers with caution as it may affect API rate limits
- The tool prefers 1080p/BluRay releases with good seeder counts
- Files are processed through Real-Debrid for safety

## Disclaimer

This information is for educational use only.  I do not condone or encourage any illegal activity, including unauthorized downloading. Streaming copyrighted content without permission may present legal risks.  You are solely responsible for your actions.