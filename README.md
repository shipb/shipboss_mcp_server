# ShipBoss MCP Server

An intelligent shipping assistant for Claude Desktop and other MCP clients. Get real-time shipping rates, create labels, track packages, and manage logistics directly in your AI conversations.

## What Can You Do?

🚚 **Get Shipping Rates**: Compare prices across FedEx, UPS, and DHL instantly  
📦 **Create Shipping Labels**: Generate professional shipping labels with tracking  
🔍 **Track Packages**: Monitor shipments in real-time across all major carriers  
🏗️ **Freight Services**: Handle heavy shipments with LTL freight options  
📅 **Schedule Pickups**: Arrange carrier pickups without phone calls  
🌍 **Smart Addressing**: Works with addresses worldwide (US, CA, EU, and more)

## Quick Examples

Just ask Claude naturally:

> *"Get shipping rates from New York to Los Angeles for a 5-pound package"*

> *"Create a FedEx Ground label from my office to 123 Main St, Chicago, IL"*

> *"Track UPS package 1Z999AA1234567890"*

> *"Schedule a pickup for tomorrow between 10 AM and 5 PM"*

## Setup Guide

### Prerequisites
- **Python 3.9+** installed on your machine
- **ShipBoss account** (sign up at [shipboss.io](https://shipboss.io))
- **API token** from your ShipBoss account settings

### Claude Desktop Setup

**Step 1**: Get your ShipBoss API token
- Sign up at [ShipBoss](https://shipboss.io)
- Go to Account Settings → API Tokens
- Generate a new token and copy it

**Step 2**: Open Claude Desktop configuration
- **macOS**: Claude Desktop → Settings → Developer → Edit Config
- **Windows**: Settings → Developer → Edit Config

**Step 3**: Add this configuration:
```json
{
  "mcpServers": {
    "shipboss": {
      "command": "pip",
      "args": ["install", "shipboss-mcp-server"],
      "env": {
        "SHIPBOSS_API_TOKEN": "your_api_token_here"
      }
    }
  }
}
```

**Alternative setup** (manual installation first):
```bash
pip install shipboss-mcp-server
```

Then use this configuration:
```json
{
  "mcpServers": {
    "shipboss": {
      "command": "shipboss-mcp-server",
      "env": {
        "SHIPBOSS_API_TOKEN": "your_api_token_here"
      }
    }
  }
}
```

**Step 4**: Save and restart Claude Desktop

**Step 5**: Verify it's working
- Look for the 🔌 icon in Claude's input area
- You should see "shipboss" listed as an available server

### Other MCP Clients

#### Cursor IDE
```json
{
  "mcpServers": {
    "shipboss": {
      "command": "pip",
      "args": ["install", "shipboss-mcp-server"],
      "env": {
        "SHIPBOSS_API_TOKEN": "your_api_token_here"
      }
    }
  }
}
```

#### General MCP Client
For any MCP-compatible client, use:
- **Package**: `shipboss-mcp-server` (from PyPI)
- **Environment**: `SHIPBOSS_API_TOKEN=your_token`

## Features in Detail

### Parcel Shipping
- **Rate Shopping**: Compare prices across FedEx, UPS, DHL
- **Smart Defaults**: Auto-detects package types and service levels
- **Label Creation**: Professional shipping labels with tracking numbers
- **Service Shortcuts**: Use "GROUND", "EXPRESS", "2DAY" instead of full names

### Address Intelligence
- **Flexible Formats**: Handles various address formats automatically
- **Global Support**: US, Canada, Mexico, Europe, and more
- **Validation**: Catches address errors before shipping

### Package Management
- **Auto-Detection**: Suggests package types based on dimensions
- **Weight Validation**: Ensures accurate shipping calculations
- **Dimension Optimization**: Recommends optimal packaging

### Tracking & Management
- **Real-Time Tracking**: Monitor packages across all carriers
- **Pickup Scheduling**: Arrange pickups without phone calls
- **Status Updates**: Get delivery status and estimated arrival

### Freight Services
- **LTL Freight**: Handle heavy/large shipments
- **Rate Quotes**: Compare freight carriers and services
- **Freight Labels**: Generate BOL and shipping documentation

## Usage Examples

### Basic Shipping
```
"I need to ship a 3-pound laptop from San Francisco to Miami. What are my options?"
```

### Complex Logistics
```
"Create shipping labels for 5 packages going to different states, all from our warehouse in Dallas. Each package is about 2 pounds, standard boxes."
```

### Freight Shipping
```
"Get freight rates for shipping 10 pallets of equipment from Chicago to Los Angeles. Each pallet weighs 500 pounds."
```

### Package Tracking
```
"Track these packages: UPS 1Z999AA1234567890, FedEx 7749-0123-4567"
```

**Ready to streamline your shipping?** Set up ShipBoss MCP and start shipping smarter with AI assistance! 🚀 