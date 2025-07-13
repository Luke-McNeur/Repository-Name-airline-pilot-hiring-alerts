# Airline Pilot Hiring Alerts

An automated RSS monitoring system that tracks U.S.-based airline pilot hiring opportunities and sends email alerts when relevant job postings are detected.

## Overview

This n8n workflow monitors multiple aviation-related RSS feeds daily and uses AI to evaluate articles for pilot hiring opportunities. When relevant opportunities are found, email alerts are automatically sent to notify about potential job openings.

## How It Works

1. **Daily Monitoring**: The system runs automatically at 8:00 AM EST each day
2. **RSS Collection**: Gathers articles from multiple aviation news sources
3. **AI Evaluation**: Uses OpenAI GPT-3.5-turbo to score each article based on hiring relevance
4. **Smart Filtering**: Only sends alerts for articles scoring 4 or higher (out of 10)
5. **Email Notifications**: Sends formatted HTML emails with relevant opportunities

## RSS Sources Monitored

### Google Alerts RSS
- **URL**: `https://www.google.com/alerts/feeds/14661532088978691670/6375579449863354933`
- **Purpose**: Custom Google Alert for airline pilot hiring keywords
- **Content**: News articles mentioning pilot hiring, recruitment, applications

### FAA Press Releases RSS
- **URL**: `https://www.faa.gov/newsroom/press_releases/rss`
- **Purpose**: Official FAA announcements and regulatory updates
- **Content**: Government aviation news, policy changes, industry updates

### AOPA RSS
- **URL**: `https://www.aopa.org/rss`
- **Purpose**: Aircraft Owners and Pilots Association news feed
- **Content**: General aviation news, industry trends, pilot-related articles

### Reddit Aviation Careers RSS
- **URL**: `https://www.reddit.com/r/aviationcareers/.rss`
- **Purpose**: Community discussions about aviation career opportunities
- **Content**: Job postings, career advice, hiring announcements, industry insights

## Scoring System

The AI agent evaluates each RSS article using the following criteria (0-10 scale):

### Positive Scoring Factors

| Factor | Points | Examples |
|--------|--------|----------|
| **Hiring Language** | +4 | "now hiring", "accepting applications", "pilot recruitment", "first officer openings" |
| **Specific U.S. Airlines** | +2 | Delta, United, American, Alaska, JetBlue, Spirit, SkyWest, Envoy |
| **Timeline/Dates** | +2 | "Fall 2025", "applications open this week", specific deadlines |
| **U.S. Relevance** | +1 | U.S. cities, .com airline links, FAA mentions, U.S.-based carriers |
| **Perks/Bonuses** | +1 | Sign-on bonus, relocation assistance, tuition reimbursement, cadet programs |

### Negative Scoring Factors

| Factor | Points | Examples |
|--------|--------|----------|
| **Unrelated Roles** | -5 | Flight attendants, airport staff, customer service, international-only hiring |

### Alert Thresholds

- **Score 4-6**: Standard alert - relevant hiring opportunity
- **Score 7-8**: High priority alert - strong hiring signal
- **Score 9-10**: Critical alert - immediate action recommended

## Email Alert Format

When qualifying articles are found, the system sends an HTML email containing:

- Article title and publication date
- Content summary/snippet
- Direct link to the original article
- Clean, professional table formatting
- Responsive design for mobile viewing

## Technical Implementation

### n8n Workflow Components

1. **Schedule Trigger**: Runs daily at 8:00 AM EST
2. **RSS Feed Readers**: Collect articles from all four sources (max 5 per source)
3. **Data Processing**: Merges and formats RSS data for AI analysis
4. **AI Agent**: OpenAI GPT-3.5-turbo with structured output parsing
5. **Conditional Logic**: Filters articles meeting score threshold
6. **Email Formatting**: Generates HTML email with responsive design
7. **Gmail Integration**: Sends alerts to specified recipients

### Key Features

- **Error Handling**: Continues processing even if individual RSS feeds fail
- **Rate Limiting**: Prevents excessive API calls
- **Data Validation**: Ensures proper formatting and content structure
- **Manual Testing**: Includes manual trigger for workflow testing

## Setup Instructions

### Prerequisites

- n8n instance (cloud or self-hosted)
- OpenAI API key
- Gmail account with OAuth2 configuration
- Access to RSS feed URLs

### Configuration Steps

1. **Import Workflow**: Import the provided n8n workflow JSON
2. **Configure Credentials**:
   - Add OpenAI API credentials
   - Set up Gmail OAuth2 authentication
3. **Update Email Recipients**: Modify recipient email addresses in Gmail node
4. **Test RSS Feeds**: Verify all RSS URLs are accessible
5. **Schedule Activation**: Enable the daily 8:00 AM trigger
6. **Test Run**: Execute manual trigger to verify functionality



## Customization Options

### Modify Scoring Criteria
Update the AI agent prompt to adjust scoring factors and weights.

### Change Schedule
Modify the Schedule Trigger to run at different times or frequencies.

### Add RSS Sources
Include additional aviation news feeds by adding new RSS Feed Read nodes.

### Adjust Alert Threshold
Change the score threshold in the conditional logic node.

### Customize Email Design
Modify the HTML template in the Gmail node for different styling.

## Monitoring and Maintenance

### Regular Checks
- Verify RSS feeds remain accessible
- Monitor OpenAI API usage and costs
- Check email delivery and formatting
- Review scoring accuracy and adjust as needed

### Troubleshooting
- Check n8n execution logs for errors
- Verify RSS feed responses
- Test OpenAI API connectivity
- Validate Gmail authentication

## Use Case

This system was built for John, a pilot seeking his first airline opportunity. The automated monitoring ensures no hiring announcements are missed while filtering out irrelevant aviation news. The scoring system prioritizes actionable opportunities, reducing noise and focusing attention on genuine job openings.

## Contributing

To improve the scoring algorithm or add new RSS sources:

1. Test changes using the manual trigger
2. Monitor alert quality over several days
3. Adjust scoring criteria based on results
4. Document any modifications

## License

This project is for personal use. Please respect RSS feed terms of service and API usage limits.
