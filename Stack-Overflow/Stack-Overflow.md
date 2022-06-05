## Introduction

Stack Overflow is one of the largest online communities for developers to learn and share their knowledge. 
The website provides a platform for its users to ask and answer questions, and through membership and active participation, to vote questions and answers up or down. Users can edit questions and answers in a fashion similar to a wiki (https://en.wikipedia.org/wiki/Wiki).
Users of Stack Overflow can earn reputation points and badges. 
For example, a person is awarded ten reputation points for receiving an “up” vote on an answer and five points for the “up” vote of a question. The can also receive badges for their valued contributions. 
A higher reputation lets users unlock new privileges like the ability to vote, comment on, and even edit other people’s posts.

## System Requirements

We will be designing a system with the following requirements:
1. Any non-member (guest) can search and view questions. However, to add or upvote a question, they have to become a member.
2. Members should be able to post new questions.
3. Members should be able to add an answer to an open question.
4. Members can add comments to any question or answer.
5. A member can upvote a question, answer or comment.
6. Members can flag a question, answer or comment, for serious problems or moderator attention.
7. Any member can add a bounty (https://stackoverflow.com/help/bounty) to their question to draw attention.
8. Members will earn badges (https://stackoverflow.com/help/badges) for being helpful.
9. Members can vote to close (https://stackoverflow.com/help/closed-questions) a question; Moderators can close or reopen any question.
10. Members can add tags (https://stackoverflow.com/help/tagging) to their questions. A tag is a word or phrase that describes the topic of the question.
11. Members can vote to delete (https://stackoverflow.com/help/deleted-questions) extremely off-topic or very low-quality questions.
12. Moderators can close a question or undelete an already deleted question.
13. The system should also be able to identify most frequently used tags in the questions.

## Use Case Diagram

We have five main actors in our system:
1. **Admin:** Mainly responsible for blocking or unblocking members.
2. **Guest:** All guests can search and view questions.
3. **Member:** Members can perform all activities that guests can, in addition to which they can add/remove questions, answers, and comments. Members can delete and un- delete their questions, answers or comments.
4. **Moderator:** In addition to all the activities that members can perform, moderators can close/delete/undelete any question.
5. **System:** Mainly responsible for sending notifications and assigning badges to members.

Here are the top use cases for Stack Overflow:
1. Search questions.
2. Create a new question with bounty and tags.
3.  Add/modify answers to questions.
4. Add comments to questions or answers.
5. Moderators can close, delete, and un-delete any question.

## Class Diagram

1. **Question:** This class is the central part of our system. It has attributes like Title and Description to define the question. In addition to this, we will track the number of times a question has been viewed or voted on. We should also track the status of a question, as well as closing remarks if the question is closed.
2. **Answer:** The most important attributes of any answer will be the text and the view count. In addition to that, we will also track the number of times an answer is voted on or flagged. We should also track if the question owner has accepted an answer.
3. **Comment:** Similar to answer, comments will have text, and view, vote, and flag counts. Members can add comments to questions and answers.
4. **Tag:** Tags will be identified by their names and will have a field for a description to define them. We will also track daily and weekly frequencies at which tags are associated with questions.
5. **Badge:** Similar to tags, badges will have a name and description.
6. **Photo:** Questions or answers can have photos.
7. **Bounty:** Each member, while asking a question, can place a bounty to draw attention. Bounties will have a total reputation and an expiry date.
8. **Account:** We will have four types of accounts in the system, guest, member, admin, and moderator. Guests can search and view questions. Members can ask questions and earn reputation by answering questions and from bounties.
9. **Notification:** This class will be responsible for sending notifications to members and assigning badges to members based on their reputations.


## Code

**Enums, data types, and constants:**

```
public enum QuestionStatus{
  OPEN,
  CLOSED,
  ON_HOLD,
  DELETED 
}
public enum QuestionClosingRemark{
  DUPLICATE,
  OFF_TOPIC,
  TOO_BROAD,
  NOT_CONSTRUCTIVE,
  NOT_A_REAL_QUESTION,
  PRIMARILY_OPINION_BASED
}
public enum AccountStatus{
  ACTIVE,
  CLOSED,
  CANCELED,
  BLACKLISTED,
  BLOCKED
}
```

**Account, Member, Admin, and Moderator:**

```
public class Account {
  private String id;
  private String password;
  private AccountStatus status;
  private String name;
  private Address address;
  private String email;
  private String phone;
  private int reputation;
  public boolean resetPassword();
}
public class Member {
  private Account account;
  private List<Badge> badges;
  public int getReputation();
  public String getEmail();
  public boolean createQuestion(Question question);
  public boolean createTag(Tag tag);
}
public class Admin extends Member {
  public boolean blockMember(Member member);
  public boolean unblockMember(Member member);
}
public class Moderator extends Member {
  public boolean closeQuestion(Question question);
  public boolean undeleteQuestion(Question question);
}
```

**Badge, Tag, and Notification:**

```
public class Badge {
  private String name;
  private String description;
}
public class Tag {
  private String name;
  private String description;
  private long dailyAskedFrequency;
  private long weeklyAskedFrequency;
}
public class Notification {
  private int notificationId;
  private Date createdOn;
  private String content;
  public boolean sendNotification();
}
```

**Photo and Bounty:**

```
public class Photo {
  private int photoId;
  private String photoPath;
  private Date creationDate;
  private Member creatingMember;
  public boolean delete();
}
public class Bounty {
  private int reputation;
  private Date expiry;
  public boolean modifyReputation(int reputation);
}
```

