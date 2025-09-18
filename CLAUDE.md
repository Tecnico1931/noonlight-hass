# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a forked and modified version of the Konnected.io Noonlight Home Assistant integration, adapted for direct Noonlight API usage for self-hosting.

**Key Differences from Original:**
- Removes dependency on Konnected.io's intermediary service
- Uses direct Noonlight API with server token authentication
- Simplified configuration without OAuth flow

## Architecture

**Main Components:**
- `custom_components/noonlight/`: Home Assistant custom component
  - `__init__.py`: Core integration logic and NoonlightIntegration class
  - `const.py`: Constants and configuration keys
  - `switch.py`: Noonlight alarm switch entity
  - `config_flow.py`: Home Assistant configuration flow UI
  - `manifest.json`: Component metadata and dependencies

**Key Classes:**
- `NoonlightIntegration`: Handles API communication and alarm management
- `NoonlightSwitch`: Home Assistant switch entity for triggering alarms

**API Integration:**
- Direct integration with Noonlight API endpoints
- Server token authentication (from developer.noonlight.com)
- Supports creating alarms with location and service type selection

## Configuration

**Required Settings:**
- Server Token: Obtained from Noonlight developer portal
- Location: Either address or latitude/longitude
- API Endpoint: `https://api.noonlight.com/platform/v1` (default)

**Location Modes:**
- Address-based: Requires street address, city, state, ZIP
- Coordinates-based: Uses latitude/longitude

## Development Notes

**Dependencies:**
- `noonlight` Python package (>=0.1.1) - may need modification for direct API usage
- Home Assistant core integration framework

**Key API Endpoints Used:**
- `POST /dispatch/v1/alarms`: Create emergency alarm
- Alarm status polling for active alarms

**Authentication:**
- Server token passed in Authorization header
- No OAuth flow required (unlike original Konnected.io version)