# Contribution [2]: Duplicate ids on same page

**Contribution Number:** 2 
**Student:** Mehereen Meem  
**Issue:** https://github.com/phpmyadmin/phpmyadmin/issues/19108  
**Status:** Phase II Update

---

## Why I Chose This Issue

I chose this issue because it’s labeled as a good first issue, newbie, and UI issue, so it seemed like a good starting point for my first open source contribution. The problem is clearly explained, and the maintainers gave helpful context and suggestions for possible fixes. I also liked that the issue involves real debugging and frontend work without being too overwhelming or requiring deep backend knowledge.

Overall, it felt like a good balance between learning how to work in a larger codebase, contributing something meaningful, and keeping the scope manageable for a first contribution.

---

## Understanding the Issue

### Problem Description

Some pages in phpMyAdmin currently have duplicate HTML id attributes. Since HTML IDs are supposed to be unique on a page, this becomes a problem when the same Twig templates get rendered multiple times and create repeated IDs in the DOM. This can cause issues with JavaScript selectors, accessibility tools, and general browser behavior because IDs are meant to identify a single element on the page.

### Expected Behavior

Each HTML element on a page should have a unique id value. If multiple elements need similar styling or behavior, they should use classes or data attributes instead of duplicate IDs. Running the duplicate ID detection script in the browser console should return an empty array with no duplicate IDs found.

### Current Behavior

Right now, when running the duplicate ID detection script from the GitHub issue, duplicate IDs are returned instead of an empty array. This means that some elements on the page are sharing the same id, which breaks standard HTML behavior.

### Affected Components

The issue appears to involve:
- Twig templates that are rendered more than once
- Frontend HTML markup
- JavaScript selectors that may depend on IDs
- UI pages such as table browsing pages where duplicate IDs appear

I will likely need to inspect the Twig templates and determine where duplicate IDs are introduced so they can be replaced or made unique safely.

---

## Reproduction Process

### Environment Setup

**System Requirements:**
- **PHP**: 8.2 or higher
- **Node.js**: 20 or higher
- **Yarn**: Latest version
- **Composer**: Latest version
- **MySQL/MariaDB**: 5.7 or higher (or any accessible database server)
- **Web Server**: Apache, Nginx, or PHP's built-in server

**Setup Steps:**

1. **Clone the repository** (if not already done):
   ```bash
   git clone https://github.com/YOUR_USERNAME/phpmyadmin.git
   cd phpmyadmin
   ```

2. **Install PHP dependencies** using Composer:
   ```bash
   composer install
   ```

3. **Install Node.js dependencies** using Yarn:
   ```bash
   yarn install
   ```

4. **Build frontend assets**:
   ```bash
      yarn run build
   ```

5. **Create configuration file** from sample:
   ```bash
   cp config.sample.inc.php config.inc.php
   ```

6. **Configure database connection** in `config.inc.php`:
   - Edit the file and set your MySQL/MariaDB connection credentials
   - Set `$cfg['Servers'][1]['host']` to your database server
   - Set `$cfg['Servers'][1]['user']` to your database user
   - Set `$cfg['Servers'][1]['password']` to your database password

7. **Start a local web server** (choose one):
   ```bash
   # Using PHP's built-in server
   php -S localhost:8000
   
   # OR using Node.js development server (if configured)
   yarn run dev
   ```

8. **Access phpMyAdmin**:
   - Open browser to `http://localhost:8000`
   - Log in with your database credentials


### Steps to Reproduce

1. Open phpMyAdmin in your browser and log in
2. Navigate to any page where query results are displayed (e.g., SQL tab with results, or Browse tab)
3. Open Browser Developer Console (F12 → Console tab)
4. Run the duplicate ID detection script:
   ```javascript
   // Find all elements with IDs
   const allElements = document.querySelectorAll('[id]');
   const idMap = new Map();
   
   // Count occurrences of each ID
   allElements.forEach(el => {
     const id = el.id;
     if (idMap.has(id)) {
       idMap.get(id).push(el);
     } else {
       idMap.set(id, [el]);
     }
   });
   
   // Find duplicates
   const duplicates = Array.from(idMap.entries())
     .filter(([id, elements]) => elements.length > 1)
     .map(([id, elements]) => ({
       id: id,
       count: elements.length,
       elements: elements
     }));
   
   console.log('Duplicate IDs found:', duplicates);
   console.table(duplicates);
   ```



1. [Step 1]
2. [Step 2]
3. [Observed result]

### Reproduction Evidence

- **Commit showing reproduction:** [Link to commit in your fork]
- **Screenshots/logs:** [If applicable]
- **My findings:** [What you discovered during reproduction]

---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** [Restate the problem]

**Match:** [What similar patterns/solutions exist in the codebase?]

**Plan:** [Step-by-step implementation plan]
1. [Modify file X to do Y]
2. [Add function Z]
3. [Update tests]

**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** [How will you verify it works?]

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
