

## 🎯 Vision
A Vacation Tracking System (VTS) will provide individual employees with the 
capability to manage their own vacation time, sick leave, and personal time off, 
without having to be an expert in company policy or the local facility’s leave 
policies

## 📋 Requirements
### ✅ Functional Requirements (FRs)
  
  1. Implements a flexible rules-based system for validating and verifying leave time requests.

  2. Enables manager approval (optional)

  3. Provides access to requests for the previous calendar year and allows requests to be made up to a year and a half in the future.
 
  4. Uses e-mail notification to request manager approval and notify employees of request status changes.

  5. Keeps activity logs for all transactions.
  
  6. Enables HR and system admin to override all actions, with logging.
  
  7. Allows managers to directly award personal leave time 
  8. Integration services 

### ✅ Non-Functional Requirements (NFRs)
  
  . * Uses existing hardware and middleware
    * The system must be easy to use.[usability]

  

## 🚧 Constraints

  * Integrations
  * Legacy Hardware 
  * Single-sign-on
  * User experience

## 📌 Domain [Define Problem]

 Many organizations lack an efficient and automated system to manage employee vacation requests and approvals. Manual methods or basic email-based systems lead to delays, errors, policy violations, and lack of transparency. There is a need for a centralized, web-based vacation tracking system that ensures accurate tracking, timely approvals, and policy compliance.

## 🎭 Actors:
 1. Managers
 2. Employees
 3. HR
 4. System Admin

# State Machine System
  ![Flow-chart](Flow-chart/StateMachine.drawio.png)

 
# Flow-chart
 ## 1. Manage Time
  ![Flow-chart](Flow-chart/Flow-chart-leaveManageTime.png)

# use-case 

 ## ManageTime (Employee , Manager)
 ## 📝Submit Request leave
 <details>
 <summary>flow chart </summary>

   ![Flow-chart](Flow-chart/EmployeeAndManagerFlow.png)
</details>

<details>
 <summary>Sequence Diagram (create Leave Request)</summary>

![sequence-digrame](sequence-digrame/createLeaveRequest.png)
</details>

 <details>
  <summary>Pseudocode</summary>

   ## 🧑‍💼 EMPLOYEE SECTION

  ```
  function createLeaveRequest:
    employeeLogin()
    selectRequestCategory()
    requestData:=FillDate()
    submitLeaveRequest(requestDate)

  function submitLeaveRequest(request):
      if isValid(request):
          saveToDatabase(request)
          notifyManager(request)
      else:
          showError("Invalid request")
  ```
  ## 🧑‍💼 Manager SECTION
  ```
  function reviewManagerRequests:
      managerLogin()
      pendingRequests := fetchPendingRequests()

      for request in pendingRequests:
      displayRequestDetails(request)
      decision := getManagerDecision() // approve or reject
      processDecision(request, decision)

  function processDecision(request, decision):
      if decision == "approve":
        updateRequestStatus(request, "Approved")
        notifyEmployee(request, "Approved")
      
      else if decision == "reject":
        updateRequestStatus(request, "Rejected")
        notifyEmployee(request, "Rejected")

      else:
        showError("Invalid decision")
  ```
</details>


 ##  Cancel Request  (Employee)
 ## ⛔ Cancel Request leave
 <details>
 <summary>flow chart </summary>

 ![Flow-chart](Flow-chart/CancelRequest.png)
</details>
<details>
 <summary>Sequence Diagram (Cancel Leave Request)</summary>

 ![sequence-digrame](sequence-digrame/cancelLeaveRequest.png)
</details>

<details>
  <summary>Pseudocode</summary>
  
  ```
  function cancelRequestLeave:
    request =:selectRequestToCancel

    if (request in "InFuture")
      valid =: displayConfirmCancel
      if(valid)
        changeAfterEmployeeCancell
      else
        return  

   else (request in "Previous 5 business days")
      valid =: displayConfirmCancelAndCancelReason
      if(valid)
        changeAfterEmployeeCancell
      else
        return  

  function changeAfterEmployeeCancell
     updateRequestToCancellInDB
     updateEmployeeBalance    
  
  ```
  </details>

 ##   Withdraw Request(Employee)
 ## ↩️  Withdraw Request
 
 <details>
 <summary>flow chart </summary>

 ![Flow-chart](Flow-chart/withdrawRequest.png)
</details>

<details>
 <summary>Sequence Diagram (withdrawRequest)</summary>

 ![sequence-digrame](sequence-digrame/withdrawRequest.png)
</details>

<details>
  <summary>Pseudocode</summary>
  
  ```
  function withdrawRequest:
      employeeLogin()
      request:= selectPendingRequest()
      selectRequestTOWithdraw()
      prompt("Do you sure to withdraw")
      if(valid)
        sendsNotificationEmail()
        updateStatusToWithdrawInDB
        removeLeaveRequestFromManager'sPendingList(leaveRequest)

      else
        NothingHappen  
  ```


### b. sequence digrame (withdraw Pending Request)
   ![sequence-digrame](sequence-digrame/withdrawLeaveRequest.png)

   ### d. sequence digrame (edit Pending Request)
   ![sequence-digrame](sequence-digrame/editLeaveRequest.png)


 