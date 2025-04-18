# Frontend Server for Generative Agents Simulation

This directory contains the Django web application responsible for the visualization and interaction layer of the generative agents human behavior simulation system.

## Purpose

The primary goal of this frontend server is to provide a web-based interface for:

*   **Visualizing Agent Behavior:** Displaying agents and their actions within the simulated environment ("The Ville").
*   **Simulation Control & Replay:** Allowing users to run simulations and view recorded replays.
*   **Agent Inspection:** Providing tools to examine agent memory, conversations, and internal cognitive states.
*   **Path Testing:** Facilitating the testing and visualization of agent navigation paths.

## Directory Structure Breakdown

```
environment/frontend_server/
├── .DS_Store             # macOS directory metadata (can be ignored)
├── Procfile              # Deployment process configuration (e.g., for Heroku)
├── README.md             # Original README file for the frontend server
├── README_generated.md   # This generated README file
├── compressed_storage/   # Stores optimized/processed simulation data for efficient replays
├── db.sqlite3            # Default Django SQLite database file (might store app state or metadata)
├── frontend_server/      # Main Django project directory
│   ├── __init__.py
│   ├── settings.py       # Django project settings
│   ├── urls.py           # Root URL configuration
│   └── wsgi.py           # WSGI entry point for web servers like Gunicorn
├── global_methods.py     # Python script with general utility functions (file I/O, etc.)
├── manage.py             # Django's command-line utility for administrative tasks
├── requirements.txt      # Lists required Python packages for the project
├── runtime.txt           # Specifies the Python runtime version (e.g., for Heroku)
├── static_dirs/          # Contains static assets (CSS, JavaScript, images, character data)
├── storage/              # Stores raw, complete simulation data (likely JSON)
├── temp_storage/         # Temporary storage for data generated during active simulations
├── templates/            # HTML templates used to render the web pages
└── translator/           # A Django app containing core logic for simulation visualization and data handling
```

## Key Files & Components

*   **`manage.py`**: The standard Django script used to run the development server (`python manage.py runserver`), apply database migrations, and perform other administrative tasks.
*   **`frontend_server/` (Directory)**: Contains the core Django project configuration, including database settings, installed apps, middleware (`settings.py`), main URL routing (`urls.py`), and the WSGI configuration (`wsgi.py`) needed to run the application with a web server.
*   **`translator/` (Directory)**: This is a Django *app* within the project. It likely holds the specific views, models (if any), and logic required to process simulation data from the storage directories and translate it into the visual format presented to the user via the HTML templates.
*   **`templates/` (Directory)**: Contains the HTML files that define the structure and layout of the web interface. Django's templating engine uses these files to generate the final HTML sent to the user's browser.
*   **`static_dirs/` (Directory)**: Stores static files required by the frontend, such as:
    *   CSS stylesheets for visual appearance.
    *   JavaScript files for client-side interactivity (potentially including the Phaser.js library mentioned in the original README for the game-like visualization).
    *   Images and other assets (e.g., character sprites, environment tiles).
*   **`storage/`, `compressed_storage/`, `temp_storage/` (Directories)**: These directories handle the simulation data persistence:
    *   `storage/`: Likely contains the full, detailed output of simulation runs.
    *   `compressed_storage/`: May contain processed or summarized data optimized for faster loading during replays.
    *   `temp_storage/`: Used for intermediate data during an active simulation before it's finalized.
*   **`global_methods.py`**: A utility module providing reusable Python functions for common tasks like reading/writing CSV files, creating folders, calculating averages/standard deviations, and copying files. These functions might be used by the `translator` app or other parts of the simulation system.
*   **`requirements.txt`**: Crucial file listing all Python dependencies. Notable entries include `Django`, `gunicorn` (web server), `openai` (suggesting potential integration with OpenAI APIs), `numpy`, `pandas`, `scikit-learn`, `matplotlib`, `seaborn` (data analysis/visualization libraries), and `nltk` (natural language processing). This indicates the server might perform significant data processing or leverage AI capabilities.
*   **`Procfile`**: Used by platforms like Heroku to know how to run the application. The line `web: gunicorn frontend_server.wsgi --timeout 600 --log-file -` specifies that the `web` process should be started using the `gunicorn` WSGI server, pointing it to the Django application's entry point (`frontend_server.wsgi`), setting a long request timeout (600 seconds), and directing logs to standard output.
*   **`runtime.txt`**: Specifies the exact Python version (`python-3.9.12`) required to run the project, ensuring consistency across environments, especially important for platform-as-a-service deployments.
*   **`db.sqlite3`**: The default database file for Django projects using SQLite. It might store user accounts, application settings, or metadata related to simulations, although the primary simulation *data* appears to be stored as files in the `storage` directories.

## How It Works (Conceptual Overview)

1.  The application is run using Django's development server (`manage.py runserver`) or a production WSGI server like Gunicorn (`Procfile`).
2.  When a user accesses the web interface, Django routes the request (based on `frontend_server/urls.py` and potentially `translator/urls.py`) to a specific *view* function within the `translator` app.
3.  The view function likely reads simulation data from the `storage/` or `compressed_storage/` directories.
4.  This data is processed (potentially using functions from `global_methods.py` or libraries like Pandas/Numpy).
5.  The processed data is passed to an HTML template located in the `templates/` directory.
6.  Django renders the template, inserting the data into the HTML structure.
7.  The final HTML, along with necessary CSS and JavaScript from `static_dirs/`, is sent to the user's browser.
8.  Client-side JavaScript (possibly using Phaser.js) might then use the embedded data or make further requests to the server to create the interactive visualization of the simulation.

## Dependencies

*   **Python:** Version 3.9.12 (as specified in `runtime.txt`)
*   **Django:** Web framework core.
*   **Gunicorn:** WSGI server for deployment.
*   **Other Python Packages:** As listed in `requirements.txt`. Includes data science, NLP, and potentially AI libraries.
*   **Client-Side:** Likely JavaScript libraries such as Phaser.js for the visualization canvas (inferred from original README).
