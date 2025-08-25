# ShipBoss MCP Server

An MCP server that provides shipping and logistics capabilities through AI conversations. Connect to FedEx, UPS, and DHL to get rates, create labels, track packages, and manage freight shipments.

> **🔑 Important**: You'll need a ShipBoss API token to use this server. Get one from your [ShipBoss Admin → API Integrations](https://ship.shipboss.io/customer-admin/api-integrations).
>
> **📁 This setup uses local development mode** with virtual environment paths for maximum compatibility and control.

## 🚀 Quick Setup (5 Minutes)

### Prerequisites
- **Python 3.9+** installed
- **ShipBoss account** with API token (get one in the admin section at [ship.shipboss.io](https://ship.shipboss.io))

### Step-by-Step Installation

**Step 1: Get Your ShipBoss API Token** 🔑
This is required for the server to communicate with ShipBoss APIs.

1. Go to [ShipBoss](https://ship.shipboss.io) and log in
2. Navigate to your Admin section → [API Integrations](https://ship.shipboss.io/customer-admin/api-integrations)
3. Generate a new API token and copy it
4. **Keep this token secure** - you'll need it in the next step

**Step 2: Create a Virtual Environment** 🐍
Using a virtual environment is **required** to avoid dependency conflicts with your system Python installation.

```bash
# Create a virtual environment
python -m venv shipboss_env

# Activate it
# Windows:
shipboss_env\Scripts\activate
# macOS/Linux:
source shipboss_env/bin/activate

# Install the package
pip install shipboss-mcp-server
```

**⚠️ Important**: Using a virtual environment is **required** to avoid dependency conflicts with your system Python installation.

**Step 3: Configure API Token** 🔑
The server needs your API token to authenticate with ShipBoss. Choose one of these methods:

#### Option A: .env File (Simplest - Automatic) 📁
```bash
# Create environment file in the project directory
echo "SHIPBOSS_API_TOKEN=your_api_token_here" > .env

# Or use the provided template
cp example.env .env  # Then edit .env with your actual token
```

Then use this configuration in your MCP client:
```json
{
  "mcpServers": {
    "shipboss-mcp": {
      "command": "C:\\path\\to\\shipboss_env\\Scripts\\python.exe",
      "args": ["C:\\path\\to\\shipboss-mcp\\shipboss_mcp_server.py"]
    }
  }
}
```

#### Option B: Command-Line Arguments
Add your token directly in the MCP configuration:
```json
{
  "mcpServers": {
    "shipboss-mcp": {
      "command": "C:\\path\\to\\shipboss_env\\Scripts\\python.exe",
      "args": [
        "C:\\path\\to\\shipboss-mcp\\shipboss_mcp_server.py",
        "--api-token", "your_api_token_here"
      ]
    }
  }
}
```

#### Option C: Environment Variable
```json
{
  "mcpServers": {
    "shipboss-mcp": {
      "command": "C:\\path\\to\\shipboss_env\\Scripts\\python.exe",
      "args": ["C:\\path\\to\\shipboss-mcp\\shipboss_mcp_server.py"],
      "env": {
        "SHIPBOSS_API_TOKEN": "your_api_token_here"
      }
    }
  }
}
```

**Note**: Replace `C:\path\to\shipboss_env` with your actual virtual environment path and `C:\path\to\shipboss-mcp` with your actual project directory path.

### How to Find Your Paths

**For Windows:**
```bash
# Find your virtual environment Python executable
cd shipboss_env\Scripts
echo %CD%\python.exe

# Find your project directory
cd ..\..
echo %CD%\shipboss_mcp_server.py
```

**For macOS/Linux:**
```bash
# Find your virtual environment Python executable
which python  # Should show the venv python path

# Find your project directory
pwd  # Current directory containing shipboss_mcp_server.py
```

**Quick verification:**
```bash
# Test that your paths work
"C:\path\to\shipboss_env\Scripts\python.exe" "C:\path\to\shipboss-mcp\shipboss_mcp_server.py" --api-token your_token_here
```



**Step 4: Test Your Setup** 🧪
Make sure your virtual environment is activated, then restart your MCP client and try these commands:
- *"Get shipping rates from New York to Los Angeles for a 2lb package"*
- *"Create a FedEx Ground label from 123 Main St, New York, NY to 456 Oak Ave, Los Angeles, CA"*

## Available Tools

- **ping** - Health check
- **get_parcel_rates** - Get parcel shipping rates
- **create_parcel_label** - Create parcel shipping labels with direct download URLs
- **track_parcel** - Track parcel shipments
- **create_pickup** - Schedule carrier pickups
- **cancel_pickup** - Cancel scheduled pickups
- **get_freight_rates** - Get freight shipping quotes
- **track_freight** - Track freight shipments

## Troubleshooting

### Common Issues:

1. **"python command not found" or "python.exe not found"** ❌: Make sure your virtual environment is activated before running the server.
   - **Solution**: Activate your virtual environment first:
     ```bash
     # Windows: shipboss_env\Scripts\activate
     # macOS/Linux: source shipboss_env/bin/activate
     ```

2. **"API token required" error** 🔐: Make sure you have your API token configured using one of these methods:
   - **Easiest**: Create a `.env` file with `SHIPBOSS_API_TOKEN=your_token` (automatically loaded)
   - Add `--api-token your_token` to the args in your MCP config
   - Set `SHIPBOSS_API_TOKEN` in the env section of your MCP config
   - **Verify your token**: Make sure it's from [ShipBoss API Integrations](https://ship.shipboss.io/customer-admin/api-integrations)

3. **".env file not found"**: The `.env` file should be in the project directory where `shipboss_mcp_server.py` is located, (or add the api key to the json config as detailed above.)
   - Check if the file exists: `ls -la .env`
   - Verify the token format: `cat .env` (should show `SHIPBOSS_API_TOKEN=your_token_here`)


4. **Command not found**: Ensure the package is installed and the `shipboss-mcp-server` command is available in your PATH.

5. **Path issues in MCP configuration**: Make sure your paths in the MCP config are correct:
   - Use the full path to your virtual environment's Python executable
   - Use the full path to your `shipboss_mcp_server.py` file
   - Ensure the paths use the correct separators (`\` for Windows, `/` for macOS/Linux)

