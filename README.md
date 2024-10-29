# ACME WI3 Process Vendor Invoices

This UiPath project automates the workflow of processing vendor invoices within the ACME System1 web application. The process includes verifying the existence of a vendor in the system, adding invoice details if the vendor exists, or notifying the Vendor-Adding Department if the vendor is not found.

## Libraries Used

This project uses the following custom libraries:
1. [**Google Search Library**](https://github.com/mnsy1/UiPath_Google): Handles Google Chrome interactions, including search and navigation to the ACME System1 website.
2. [**ACME System1 Website Library**](https://github.com/mnsy1/UiPath_ACMESystem1): Manages all automation activities within the ACME System1 web application.

## Process Workflow

### 1. Open ACME System1 Website
- Launches Google Chrome and searches for the ACME System1 website.
- Navigates to the website.

### 2. Login to ACME System1
- Ensures the user is logged out, if needed.
- Logs in to System1 using the provided credentials.

### 3. Access Work Items
- Navigates to the Work Items page and lists all tasks available for processing.

### 4. Process WI3 Vendor Invoices
For each WI3 work item:
- Opens the details page of the work item and downloads the associated PDF invoice.
- Extracts all relevant information from the PDF.

### 5. Search and Validate Vendor
- Returns to System1's “Search for Vendors” section.
- Searches for the vendor based on the TaxID from the invoice.
    - **If the TaxID is missing**: Rejects the work item and comments “TaxID missing; cannot process.”
    - **If the Vendor is found**:
        - Accesses the “Add Invoice Details” section.
        - Fills in all fields with extracted information.
        - Updates the work item status to “Completed” with the comment “Added Invoice [invoice-number] to system.”
    - **If the Vendor is not found**:
        - Sends an email to `vdd@acme-test.com` with the subject “Please add Vendor” and attaches the invoice.
        - Updates the work item status to “Rejected” with the comment “Vendor with TaxID [invoice-number] not found; email sent to VDD.”

### 6. Repeat for Remaining WI3 Items
- Continues the process for all WI3 items in the queue.

## Conclusion

The **ACME WI3 Process Vendor Invoices** project enables efficient automation of vendor invoice processing in the ACME System1 environment. Through structured validation and task handling, this automation reduces manual input, ensures accurate data entry, and helps maintain organized workflows within the Accounts Payable department.

## Prerequisites
- UiPath Studio (latest version)
- Google Chrome browser
- Valid credentials for ACME System1
- Email access for notification requirements

---

This README file is structured to provide a clear overview of the automation process, including key steps and exception handling.
