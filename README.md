# FantasyFootballTeamOptimizer
Returns expected points, floor and ceiling for each player in the league (on your team, on other teams, and free agents) - Still working on several improvements

Python

Step 1: Setup Environment

    Install Python:
        Ensure Python (version 3.6 or higher) is installed on your system. Download it from the official Python website: www.python.org.
	Make sure to check the box "Add Python.exe to PATH" during installation (at the bottom, where you can select "Install Now" or "Customize installation").

    Run cmd as administrator, set Up a Virtual Environment:
	cd c:\program files

	python -m venv sleeper_env

	This creates a virtual environment named sleeper_env.

	Activate the Virtual Environment:

	    On Windows:

		sleeper_env\Scripts\activate

	    On macOS/Linux:

	        source sleeper_env/bin/activate

Step 2: Install Required Libraries
	
	Each script uses Python libraries like requests, BeautifulSoup, and pandas. Install these by running:

	pip install requests beautifulsoup4 pandas sleeper_wrapper

	These libraries are used in the scripts for making API calls, parsing HTML, and handling CSV files.

Step 3: Save and Organize Files

    go to a folder C:\Program Files\sleeper_env\Scripts for the project, create inside scripts folder History (in scripts now it is C:\Program Files\sleeper_env\Scripts, while folder C:\Program Files\sleeper_env\Scripts\History is created to log data).
    Save the three scripts in this folder:
        sleeper_api_DST.py
        sleeper_api_K.py
        sleeper_api_RB_QB_TE_WR.py
	sleeper_api_get_all_players.py
	sleeper_api_get_roster.py
	sleeper_api_schedule.py

Step 4: Running the Scripts
	
	These scripts require command-line arguments for position, year, week, and scoring_system.

	Example commands to run the scripts:

		sleeper_api_schedule.py 2024 (just once)

		sleeper_api_K.py K 2024 13 PPR
		sleeper_api_DST.py DST 2024 13 PPR
		sleeper_api_RB_QB_TE_WR.py RB 2024 13 PPR
		sleeper_api_RB_QB_TE_WR.py QB 2024 13 PPR
		sleeper_api_RB_QB_TE_WR.py TE 2024 13 PPR
		sleeper_api_RB_QB_TE_WR.py WR 2024 13 PPR
		sleeper_api_get_all_players.py 13
		sleeper_api_get_roster.py 13

Arguments:

    position: Player position (e.g., DST for defenses, K for kickers).
    year: Year of the data.
    week: Week number (e.g., 1, 2, 3).
    scoring_system: Scoring type (e.g., PPR, Standard).

script sleeper_api_get_roster.py has hardcoded Sleeper league ID, replace it with yours

Step 5: Verify Outputs

    Check CSV Outputs:
        CSV files are saved in the specified directory (e.g., C:\Program Files\sleeper_env\Scripts and C:\Program Files\sleeper_env\Scripts\History).
        File names will include details like position, year, week, and scoring system.

    Logs:
        Each script prints messages to the terminal indicating success or errors during execution.

Optional Steps for Troubleshooting

    Check Internet Connection: The scripts fetch data from external websites using requests. Ensure your machine is online.
    Inspect API Keys and Endpoints: If any API request fails, verify the API keys or endpoints used in the scripts.
    Adjust File Paths: Update paths in the scripts (e.g., output directories) to match your system setup.

This process should allow you to execute the scripts and retrieve the desired data! Let me know if you encounter issues.

SQL SERVER:

Step 1: Set Up Your Environment
	Install Microsoft SQL Server:

		Download the SQL Server Developer Edition from the official Microsoft website (https://www.microsoft.com/en-us/sql-server/sql-server-downloads).

		Install the database engine and configure the server.
	Install SSMS:

		Download SQL Server Management Studio 18 or later from the official download page (https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
		Install the software on your local machine.

	Ensure Necessary Permissions:
	
		Verify that you have administrator access to the SQL Server instance.

Step 2: Prepare to Run Scripts
	Open SQL Server Management Studio.
	Create new database (Databases - > New database) named eg. sleeper_fantasy

Step 3: Load and Execute the Scripts
Open the SQL Files:

In SSMS, click on File → Open → File, and select the .sql files you uploaded (Insert Analytics.sql, Insert Import and Stage.sql, Insert Pool.sql).
Review the Scripts:
----------------
Ensure the scripts reference the correct database (USE statement).
Check for placeholders or variables like <YourTableName> that need substitution.
Execute the Scripts:

Press F5 or click Execute to run the script.
Step 4: Verify Execution

insert trade and fix data from csv data into tables

    BULK INSERT [import_area_footballdb_sleeper_fix]
    FROM 'C:\Program Files\sleeper_env\Scripts\import_area_footbaldb_sleeper_fix.csv'
    WITH (
        FIELDTERMINATOR = ';',  -- Columns are separated by commas
        ROWTERMINATOR = '\n',   -- Rows are separated by newlines
        FIRSTROW = 2            -- Skip the header row
    );

    BULK INSERT [import_area_trades]
    FROM 'C:\Program Files\sleeper_env\Scripts\import_area_trades.csv'
    WITH (
        FIELDTERMINATOR = ';',  -- Columns are separated by commas
        ROWTERMINATOR = '\n',   -- Rows are separated by newlines
        FIRSTROW = 2            -- Skip the header row
    );

run "execute scripts"
