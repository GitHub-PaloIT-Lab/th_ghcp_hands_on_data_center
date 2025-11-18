# 📝 วิธี Implement Story (ฉบับเข้าใจง่าย)

## 🚀 เริ่มต้นอย่างไร?

### ขั้นตอนที่ 1: อ่านและเข้าใจ Story
```markdown
1. อ่าน Story Summary ให้เข้าใจว่าต้องทำอะไร
2. ดู Acceptance Criteria (AC) แต่ละข้อ
3. เช็ค Definition of Done ว่าต้องทำอะไรบ้าง
4. ดู Priority และ Story Points เพื่อวางแผนเวลา
```

### ขั้นตอนที่ 2: วิเคราะห์งาน
```markdown
1. แบ่ง AC เป็นงานย่อยๆ
2. เรียงลำดับความสำคัญ
3. ประเมินเวลาที่ต้องใช้
4. เตรียม test cases
```

### ขั้นตอนที่ 3: เริ่ม Implement
```markdown
1. สร้าง branch ใหม่: feature/STORY-XXX
2. เริ่มจาก AC ที่ง่ายที่สุด
3. ทำทีละ AC จนครบ
4. เขียน E2E tests
5. ทดสอบทั้งหมด
```

## ✅ Checklist ก่อนเริ่มทำ

### 📋 เช็คความพร้อม
- [ ] อ่าน Story และ AC ครบทุกข้อแล้ว
- [ ] เข้าใจ Business Value และ User Journey
- [ ] เตรียม development environment แล้ว
- [ ] รู้ว่าจะ test อย่างไร
- [ ] มี branch สำหรับ story นี้แล้ว

### 🎯 เช็คขอบเขตงาน
- [ ] รู้ว่า AC ไหนต้องทำ UI
- [ ] รู้ว่า AC ไหนต้องทำ logic
- [ ] รู้ว่าต้องเก็บข้อมูลอย่างไร
- [ ] รู้ว่าต้อง validate อะไรบ้าง
- [ ] รู้ว่าต้องจัดการ error อย่างไร

## 🛠 Template การเขียนโค้ด

### Template สำหรับ AC แต่ละข้อ
```markdown
## AC[X]: [ชื่อ AC]

### 📝 สิ่งที่ต้องทำ:
- [ ] สร้าง UI components
- [ ] เขียน business logic
- [ ] เพิ่ม validation
- [ ] จัดการ error handling
- [ ] เขียน unit tests
- [ ] เขียน E2E tests

### 🎨 UI Components:
- Component ที่ต้องสร้าง: [รายชื่อ]
- Props ที่ต้องรับ: [รายการ]
- Events ที่ต้องจัดการ: [รายการ]

### 🧠 Business Logic:
- Functions ที่ต้องเขียน: [รายชื่อ]
- Data validation: [กกฎที่ต้องเช็ค]
- Error cases: [กรณีที่อาจผิดพลาด]

### ✅ Test Cases:
- Happy path: [กรณีที่ใช้งานปกติ]
- Edge cases: [กรณีขอบเขต]
- Error cases: [กรณีที่เกิดข้อผิดพลาด]
```

### Template สำหรับ E2E Tests
```javascript
describe('STORY-XXX: [ชื่อ Story]', () => {
  beforeEach(() => {
    // Setup test data
  });

  describe('AC1: [ชื่อ AC]', () => {
    it('should [สิ่งที่ต้องเกิดขึ้น] when [เงื่อนไข]', () => {
      // Given: เตรียมสถานการณ์
      
      // When: ทำการกระทำ
      
      // Then: ตรวจสอบผลลัพธ์
    });

    it('should handle error when [เงื่อนไขที่ผิดพลาด]', () => {
      // Test error scenarios
    });
  });
});
```

## 🎯 วิธีเช็คว่าทำเสร็จแล้ว

### 📋 Checklist สำหรับแต่ละ AC
```markdown
### AC[X] Complete Checklist:
- [ ] Feature ทำงานได้ตาม AC
- [ ] UI/UX ใช้งานสะดวก
- [ ] Validation ทำงานถูกต้อง
- [ ] Error handling แสดงข้อความเข้าใจง่าย
- [ ] Unit tests ผ่านหมด
- [ ] E2E tests ผ่านหมด
- [ ] ไม่มี console errors
- [ ] Performance ยอมรับได้
```

### 🧪 E2E Testing Checklist
```markdown
- [ ] ทุก User Journey ทำงานได้
- [ ] ทดสอบใน browser หลักๆ
- [ ] ทดสอบกับข้อมูลจริง
- [ ] ทดสอบ edge cases
- [ ] ทดสอบ error scenarios
- [ ] ทดสอบ responsive design
- [ ] ทดสอบ accessibility basics
```

### 🏁 Story Complete Checklist
```markdown
- [ ] ทุก AC implement เสร็จแล้ว
- [ ] ทุก test ผ่านหมด
- [ ] Code review ผ่านแล้ว
- [ ] Documentation อัพเดทแล้ว
- [ ] Ready สำหรับ demo
- [ ] ตรงตาม Definition of Done
```

## 📚 Quick Reference สำหรับแต่ละ Story

### STORY-001: Basic Todo Management
```markdown
🎯 Focus: CRUD operations, simple UI
📝 Key ACs: Create, Read, Update, Delete, Mark Complete
🧪 E2E Priority: Create task → Mark complete → Delete
⚠️ จุดสำคัญ: Data validation, Confirmation dialogs
```

### STORY-002: Search and Filtering
```markdown
🎯 Focus: Search functionality, Filter UI
📝 Key ACs: Keyword search, Status filter, Date filter, Clear filters
🧪 E2E Priority: Search → Filter → Combine → Clear
⚠️ จุดสำคัญ: Search performance, Filter combinations
```

### STORY-003: Data Quality & Reliability
```markdown
🎯 Focus: Validation, Error handling, Data safety
📝 Key ACs: Validation, Duplicate detection, Reliable operations, Error handling
🧪 E2E Priority: Validation errors → Recovery scenarios → Data safety
⚠️ จุดสำคัญ: User-friendly error messages, Data consistency
```

### STORY-004: Demo Simulation
```markdown
🎯 Focus: Sample data, Demo flow, Realistic scenarios
📝 Key ACs: Pre-loaded data, Realistic variety, Smooth demo flow
🧪 E2E Priority: Demo scenarios → All features working smoothly
⚠️ จุดสำคัญ: Demo data quality, Performance during demo
```

## 🎭 E2E Testing Strategy

### 🎬 Test Scenarios ตาม User Journey

#### New User Experience
```gherkin
Feature: New User First Time Use
  Scenario: User creates their first task
    Given I am a new user with no tasks
    When I create my first task "Buy milk"
    Then I should see the task in my list
    And the task should show "Not Started" status
```

#### Daily Usage Patterns
```gherkin
Feature: Daily Task Management
  Scenario: User manages tasks throughout the day
    Given I have several tasks for today
    When I mark some tasks as complete
    And I add new urgent tasks
    Then my task list should reflect all changes
    And completed tasks should look different
```

#### Advanced Features
```gherkin
Feature: Power User Workflows
  Scenario: User searches and filters large task list
    Given I have 50+ tasks in various states
    When I search for "meeting" and filter by "today"
    Then I should see only relevant tasks
    And search results should be highlighted
```

### 🔧 E2E Test Setup
```javascript
// cypress/support/commands.js
Cypress.Commands.add('createTask', (title, description) => {
  cy.get('[data-cy=add-task-button]').click();
  cy.get('[data-cy=task-title]').type(title);
  cy.get('[data-cy=task-description]').type(description);
  cy.get('[data-cy=save-task]').click();
});

Cypress.Commands.add('markTaskComplete', (taskTitle) => {
  cy.contains('[data-cy=task-item]', taskTitle)
    .find('[data-cy=complete-checkbox]')
    .click();
});
```

### 📊 Test Data Management
```javascript
// cypress/fixtures/sample-tasks.json
{
  "basicTasks": [
    {
      "title": "Morning standup meeting",
      "description": "Daily team sync at 9 AM",
      "status": "not-started",
      "dueDate": "today"
    }
  ],
  "demoTasks": [
    // Pre-loaded tasks for demo scenarios
  ]
}
```

## 🚀 การใช้งาน Prompt นี้

### วิธีใช้:
1. เลือก Story ที่จะทำ (เช่น STORY-001)
2. อ่าน Quick Reference สำหรับ story นั้น
3. ทำตาม Checklist ทีละขั้นตอน
4. ใช้ Template เพื่อเขียนโค้ดและ tests
5. เช็คความสมบูรณ์ก่อน submit

### Tips สำหรับความสำเร็จ:
- **เริ่มจาง่ายก่อน** - ทำ AC ที่ง่ายที่สุดก่อน
- **Test ตลอดเวลา** - อย่ารอให้เสร็จหมดค่อย test
- **Think like user** - คิดในมุมของคนใช้งานจริง
- **Document as you go** - เขียน docs ไปพร้อมๆ กับโค้ด

---
*📝 Prompt นี้ออกแบบให้ใช้งานง่าย เข้าใจได้ทันที และครอบคลุมทุก story ใน Todo Application*