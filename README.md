# Online TRAT System
Quickly set up a Google based Team Readiness Assessment Test (TRAT) to use in school, university or training courses. This can be used for in person or online courses. 

# Digital Team Readiness Assessment Test (TRAT) System

A web-based implementation of the Team Readiness Assessment Test (TRAT) that replicates the traditional scratch card experience digitally. This system allows instructors to create multiple-choice quizzes with unique scoring mechanics and automatically collect results in Google Sheets.

## 🎯 Features

- **Authentic TRAT Experience**: Replicates traditional scratch card TRATs with 4→2→1→0 point scoring
- **Multi-TRAT Support**: One system handles unlimited different TRATs
- **Real-time Results**: Automatic data collection in Google Sheets
- **Mobile Friendly**: Works on any device with a web browser
- **Zero Cost**: Built entirely on free Google services
- **Easy Management**: Simple spreadsheet-based question management
- **Canvas Integration Ready**: Results format designed for easy grade import

## 📊 How TRAT Scoring Works

Each question has 4 multiple choice options. Students:
1. **First attempt**: If correct → 4 points
2. **Second attempt**: If correct → 2 points  
3. **Third attempt**: If correct → 1 point
4. **Fourth attempt**: If correct → 0 points

Students see immediate feedback after each attempt but can only see remaining options for subsequent attempts.

## 🚀 Quick Start

### Prerequisites
- Google account (free)
- Web browser
- 2-3 hours for initial setup

### Setup Overview
1. Create Google Sheets structure
2. Set up Google Apps Script backend
3. Deploy web application
4. Add your first TRAT
5. Share with students

## 📋 Detailed Setup Instructions

### Step 1: Create Google Sheets Structure

1. **Create a new Google Spreadsheet**
   - Go to [sheets.google.com](https://sheets.google.com)
   - Click "Blank" to create new spreadsheet
   - Name it "TRAT Master System"

2. **Set up TRAT Library Sheet**
   - Rename "Sheet1" to "TRAT_Library"
   - Add these column headers in row 1:
     ```
     A: TRAT_ID
     B: Question_Number  
     C: Question_Text
     D: Option_A
     E: Option_B
     F: Option_C
     G: Option_D
     H: Correct_Answer
     ```
   - Format headers (bold, light gray background)

3. **Set up Results Sheet**
   - Add new sheet named "Results"
   - Add these column headers in row 1:
     ```
     A: Timestamp
     B: Student_Name
     C: TRAT_ID
     D: Total_Points
     E-V: Q1_Points through Q18_Points
     ```

4. **Configure Sharing**
   - Click "Share" button
   - Change access to "Anyone with the link"
   - Set permission to "Editor"
   - Copy the sharing link

5. **Get your Spreadsheet ID**
   - From the URL: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID_HERE/edit#gid=0`
   - Copy the long string between `/d/` and `/edit`

### Step 2: Set Up Google Apps Script

1. **Open Apps Script**
   - In your spreadsheet: Extensions → Apps Script
   - Delete existing code

2. **Add the backend code**
   - Copy the code from `backend.js` (see file in repository)
   - Replace `YOUR_SPREADSHEET_ID` with your actual spreadsheet ID

3. **Add the frontend code**
   - Click "+" next to Files → HTML
   - Name it "index"
   - Copy the code from `index.html` (see file in repository)

4. **Test and Deploy**
   - Save the project
   - Run `testConnection` function to verify setup
   - Deploy as web app:
     - Click Deploy → New deployment
     - Type: Web app
     - Execute as: Me
     - Who has access: Anyone
   - Copy the web app URL

### Step 3: Add Your First TRAT

Add sample questions to test the system:

| TRAT_ID | Question_Number | Question_Text | Option_A | Option_B | Option_C | Option_D | Correct_Answer |
|---------|----------------|---------------|----------|----------|----------|----------|----------------|
| test1 | 1 | What is 2 + 2? | 3 | 4 | 5 | 6 | B |
| test1 | 2 | Which planet is closest to the sun? | Earth | Mars | Mercury | Venus | C |
| test1 | 3 | What color do you get when mixing red and blue? | Green | Purple | Orange | Yellow | B |

### Step 4: Test Your System

1. Open your web app URL
2. Enter name: "Test Student"
3. Enter TRAT code: "test1"
4. Complete the quiz
5. Verify results appear in your Results sheet

## 💻 Usage Instructions

### For Instructors

**Creating a New TRAT:**
1. Add questions to the TRAT_Library sheet
2. Use a unique TRAT_ID for each quiz
3. Number questions sequentially
4. Set correct answers as A, B, C, or D

**Sharing with Students:**
- **Generic URL**: Students enter TRAT code manually
  ```
  https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec
  ```
- **Direct URL**: TRAT code embedded in URL
  ```
  https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec?trat=YOUR_TRAT_CODE
  ```

**Managing Results:**
- View real-time results in the Results sheet
- Filter by TRAT_ID to see specific quiz results
- Export data for Canvas grade import

### For Students

1. Click the TRAT link provided by instructor
2. Enter your full name
3. Enter TRAT code (if not embedded in URL)
4. Answer each question, using multiple attempts as needed
5. View your final score when complete

## 🏗️ Repository Structure

```
trat-system/
├── README.md
├── backend.js          # Google Apps Script backend code
├── index.html          # Frontend web application
├── docs/
│   ├── setup-guide.md
│   ├── troubleshooting.md
│   └── examples/
│       └── sample-questions.csv
└── screenshots/
    ├── setup-process/
    └── student-experience/
```

## 🔧 Customization

### Modifying Scoring
To change the point values (currently 4→2→1→0), edit the `getPointsForAttempt` function in `index.html`:

```javascript
function getPointsForAttempt(attempt) {
    switch(attempt) {
        case 1: return 4;  // Change these values
        case 2: return 2;
        case 3: return 1;
        case 4: return 0;
        default: return 0;
    }
}
```

### Styling
Modify the CSS in `index.html` to match your institution's branding.

### Question Limits
The system supports up to 18 questions per TRAT. To increase this limit, add more columns to the Results sheet and update the `saveResults` function.

## 🐛 Troubleshooting

### Common Issues

**"Cannot read properties of null" error:**
- Check that your spreadsheet ID is correct
- Verify sheet names are exactly "TRAT_Library" and "Results"
- Ensure spreadsheet sharing is set to "Anyone with the link" with "Editor" permissions

**Questions not loading:**
- Verify TRAT_ID matches exactly (case-sensitive)
- Check that questions have sequential question numbers
- Ensure correct answer values are exactly "A", "B", "C", or "D"

**Results not saving:**
- Check spreadsheet permissions
- Verify the Results sheet exists and has proper headers
- Check browser console for JavaScript errors

**Students can't access:**
- Ensure web app is deployed with "Anyone" access
- Check that the URL is complete and correct
- Verify students are using a compatible browser

### Getting Help

1. Check the browser console for error messages
2. Review the Google Apps Script execution logs
3. Verify all setup steps were completed exactly as described
4. Test with sample data before using with students

## 📚 Best Practices

### For Instructors
- Always test new TRATs before sharing with students
- Use descriptive TRAT_IDs (e.g., "midterm1", "chapter3quiz")
- Keep a backup copy of your questions
- Monitor the Results sheet during active TRATs

### For System Administration
- Regularly backup your Google Sheets
- Keep the Apps Script project organized
- Document any customizations you make
- Test the system periodically to ensure continued functionality

## 🔒 Privacy and Security

- Student names are stored in your Google Sheets
- No authentication is required (name-based identification only)
- All data remains in your Google account
- Consider your institution's privacy requirements before deployment

## 📄 License

This project is released under the MIT License. Feel free to modify and distribute according to your needs.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues, feature requests, or pull requests.

## 📞 Support

For technical issues:
1. Check the troubleshooting section above
2. Review Google Apps Script documentation
3. Submit an issue in this repository

## 📈 Future Enhancements

Potential improvements for future versions:
- Student authentication integration
- Advanced analytics and reporting
- Question randomization
- Time limits for questions
- Bulk question import tools
- Integration with other LMS platforms

---

**Built with ❤️ for education**

*This system was designed to help instructors easily implement Team Readiness Assessment Tests in digital learning environments while maintaining the pedagogical benefits of the traditional TRAT format.*
