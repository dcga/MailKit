# Release Notes

### MailKit 1.3.0

* Added support for dnxcore50.

### MailKit 1.2.17

* Exposed MailKit.Search.OrderByType and MailKit.Search.SortOrder to the public API.
* Modified IMailFolder.CopyTo() and MoveTo() to return a UniqueIdMap instead of a UniqueIdSet.
* Improved ImapProtocolException error messages to be more informative.
* Added an IsSecure property to ImapClient, Pop3Client and SmtpClient.
* Fixed support for the IMAP COMPRESS=DEFLATE extension to work properly.
* Modified UniqueId.Id and .Validity to be properties instead of fields.
* Reduced memory usage for UniqueIdRange (-33%) and UniqueIdSet (-50%).
* Vastly improved the performance of UniqueIdSet (~2x).
* Added an ImapClient.GetFolders() overload that also requests the status of each folder.
* Modified the headersOnly parameter to the various Pop3Client.GetStream() methods to default to
  false instead of forcing developers to pass in a value.
* Updated the IMAP, POP3 and SMTP clients to be stricter with validating SSL certificates.

### MailKit 1.2.16

* Added support for the SCRAM-SHA-256 SASL mechanism.
* Added support for the CREATE-SPECIAL-USE IMAP extension.
* Added support for the METADATA IMAP extension.
* Added support for the LIST-STATUS IMAP extension.

### MailKit 1.2.15

* Be more forgiving during SASL auth when a POP3 server sends unexpected text after a + response.
  (issue #268)

### MailKit 1.2.14

* Fixed ImapFolder.Search() to not capitalize the date strings in date queries. (issue #252)
* Fixed filtering logic in ImapFolder.GetSubfolders() to not filter out subfolders named Inbox.
  (issue #255)
* Exposed SmtpClient.ProcessRcptToResponse() as virtual protected to allow subclasses to override
  error handling. (issue #256)
* Modified SmtpCommandException .ctors to be public and fixed serialization logic. (issue #257)
* Added workaround for broken smtp.sina.com mail server.
* Throw a custom ImapProtocolException on "* BYE" during connection instead of "unexpected token".
  (issue #262)

### MailKit 1.2.13

* Fixed SmtpClient to not double dispose the socket.
* Added a BodyPartVisitor class.
* Fixed ImapFolder to allow NIL tokens for body parts. (issue #244)

### MailKit 1.2.12

* Allow developers to specify a local IPEndPoint to use for connecting to remote servers.
  (issue #247)
* Added support for NIL GMail labels. (issue #244)

### MailKit 1.2.11.1

* Fixed ImapFolder.GetSubfolders() to work with Yahoo! Mail and other IMAP servers that
  do not use the canonical INBOX naming convention for the INBOX folder. (issue #242)

### MailKit 1.2.11

* Fixed SmtpStream logic for determining if a call to ReadAhead() is needed. (issue #232)
* Fixed ImapFolder.Close() to change the state to Closed even if the IMAP server does not
  support the UNSELECT command.
* Allow the UIDVALIDITY argument to the COPYUID and APPENDUID resp-codes to be 0 even though
  that value is llegal. Improves compatibility with SmarterMail. (issue #240)

### MailKit 1.2.10

* Added an SslProtocols property to ImapClient, Pop3Client, and SmtpClient to allow
  developers to override which SSL protocols are to be allowed for SSL connections.
  (issue #229)
* Added a work-around for GMail IMAP (and other IMAP servers) that sometimes send an
  illegal MODSEQ value of 0. (issue #228)

### MailKit 1.2.9

* Fixed ImapFolder.Append() methods to make sure to encode the message with <CR><LF>
  line endings.
* Added UniqueId.Invalid that can be used for error conditions.
* Added UniqueId.IsValid property to check that the UniqueId is valid.
* Added Opened and Closed events to IMailFolder.
* Fixed the QRESYNC version of the IMailFolder.Open() method to take a uint uidValidity
  instead of a UniqueId uidValidity argument for consistency.
* Updated MessageSorter.Sort() to be an extension method and added a List<T> overload.
* Updated MessageThreader.Thread() to be extension methods (required reordering of args).
* Merged ISortable and IThreadable interfaces into IMessageSummary in order to
  remove duplicated properties and simplify things.
* Renamed IMessageSummary.MessageSize to IMessageSummary.Size.
* Modified IMessageSummary.UniqueId to no longer be nullable.
* Added TextBody, HtmlBody, BodyParts and Attachments properties to IMessageSummary.
* Modified the IMAP parser to allow NIL for the Content-Type and subtype strings in
  BODY and BODYSTRUCTURE values even though it is illegal. (issue #226)
* Modified the IMAP parser to properly handle Message-Id tokens that are not properly
  encapsulated within angle brackets. (issue #224)
* Fixed IMAP to properly deal with folder names that contained unescaped square brackets.
  (issue #222)

### MailKit 1.2.8

* Fixed ImapFolder to dispose the temporary streams used in GetMessage and GetBodyPart.
* Added a MessageNotFoundException.
* Added an ImapCommandResponse property to ImapCommandException.
* Fixed SmtpClient to filter out duplicate recipient addresses in RCPT TO.
* Modified MessageSorter/Threader to take IList<OrderBy> arguments instead of OrderBy[].
* Added support for parsing group addresses in IMAP ENVELOPE responses.
* Disable SASL-IR support for the LOGIN mechanism. (issue #216)
* Capture whether or not the IMAP server supports the I18NLEVEL and LANGUAGE extensions.

### MailKit 1.2.7

* Fixed ImapFolder.Rename() to properly emit the Renamed event for child folders as well.
* Fixed ImapFolder.Fetch() to always fill in the Headers property when requesting specific
  headers even if the server replies with an empty list. (issue #210)

### MailKit 1.2.6

* Fixed UniqueIdSet.CopyTo() to work properly (also fixes LINQ usage).
* Fixed ImapFolder.Status() where StatusItems.HighestModSeq is used.

### MailKit 1.2.5

* Added support for extended IMAP search options (see the SearchOptions flags).
* Added TryParse() convenience methods for UniqueIdSet, UniqueIdRange, and UniqueId.
* Added a workaround for a GMail IMAP BODYSTRUCTURE bug. (issue #205)
* Added a ProtocolLogger property for ImapClient, Pop3Client, and SmtpClient.
* Fixed the ImapFolder.GetStream() methods that take a BodyPart to call the
  proper overload.

### MailKit 1.2.4

* Updated SmtpClient to use MimeMessage.Prepare() instead of implementing its own logic.
* Added a new ITransferProgress interface and updated IMAP, POP3 and SMTP methods to
  take an optional ITransferProgress parameter to allow for progress reporting.
* Implemented client-side UID EXPUNGE for IMAP servers that do not support the UIDPLUS
  extension.
* Improved API documentation.

### MailKit 1.2.3

* Fixed ImapFolder.AddFlags() to throw FolderNotOpenException if the folder is not
  opened in read-write mode. (issue #202)
* Fixed ImapFolder.GetMessage/BodyPart/Stream() to not modify a dictionary while
  looping over it. (issue #201)
* Fixed ImapFolder to throw FolderNotFoundException instead of ArgumentException
  when the command fails due to the folder not existing.

### MailKit 1.2.2

* Added ImapClient.GetFolders(FolderNamespace, ...) to allow getting the full
  (recursive) list of folders for a particular namespace.
* Added a FolderAttributes.Inbox flag that gets set on the Inbox folder.
* Fixed the IMAP code to properly treat the INBOX folder name case-insensitively.
* Added ServiceNotConnectedException, ServiceNotAuthenticatedException, and
  FolderNotOpenException as a more specific errors than InvalidOperationException.
  (Note: they all subclass InvalidOperationException so old code continues to work).
* Added Pop3Client.GetStream() to allow fetching messages or headers as an unparsed
  stream. (issue #198)
* Fixed usage of Socket.Poll() to not loop 1000 times per second.
* Added more ImapFolder.GetStream() overloads.
* Added ImapFolder.CreateStream() and CommitStream() protected methods which are meant
  for subclasses that intend to implement caching.

### MailKit 1.2.1

* Added hooks to allow subclassing ImapFolder.

### MailKit 1.2.0

* Added new ImapFolder.GetStream() overloads that allow fetching only the TEXT
  stream.
* Fixed ImapFolder.Search() to always treat the search results as UIDs even
  when the server (such as AOL) does not include the required UID tag in the
  ESEARCH response. (issue #191)
* Fixed ImapClient to set the engine.Uri even for Windows*81 profiles (fixes
  a NullReferenceException for the various Windows*81 profiles). (issue #192)
* Work around a GMail bug where it does not quote flags containing []'s.
  (issue #193)
* Fixed the IMAP code to accept GMail label names that start with a '+'.
  (issue #195)
* Delay throwing ProtocolException due to an unexpected disconnect when reading
  responses to PIPELINE'd SMTP commands in case one of the responses to those
  commands contains an error code that might hint at why the server disconnected.
  (issue #194)

### MailKit 1.0.17

* Fixed a STARTTLS regression in SmtpClient that was introduced in 1.0.15.
  (issue #187)

### MailKit 1.0.16

* Modified the Pop3Client to immediately query for the message count once the
  client is authenticated. This allows the Pop3Client to now have a Count
  property that replaces the need for calling GetMessageCount(). (issue #184)

### MailKit 1.0.15

* Added SearchQuery.HeaderContains() and obsoleted SearchQuery.Header() for
  API consistency.
* Added workaround for GMail's broken FETCH command parser that does not accept
  aliases. (issue #183)

### MailKit 1.0.14

* Added a ServerCertificateValidationCallback property to all clients so that
  it is not necessary to set the global
  System.Net.ServicePointManager.ServerCertificateValidationCallback property.
* Fixed MailService.Connect(Uri) to properly handle Uri's with Port value that
  had not been explicitly set. (issue #170)
* Added logic to properly handle MODSEQ-based search responses.
  (issue #166 and issue #173)
* When an ImapClient gets disconnected, if an ImapFolder was in an opened state,
  update its state to closed to prevent confusion once the ImapClient is
  reconnected.
* Fixed a bug in Pop3Client.Authenticate() for servers that just reply with
  "+OK\r\n" to the SASL challenge. (issue #171)
* Clear the POP3 capability flags if the POP3 server responds with -ERR at
  any time. Some servers will reply with a list of capabilities until the
  client is authenticated, and then reply with -ERR meaning that the client
  should not attempt to use previously listed capabilities. (issue #174)

### MailKit 1.0.13

* Added a FileName convenience property to BodyPartBasic which works the same
  way as the MimeKit.MimePart.FileName property.
* Added a MessageSummaryFetched event to IMailFolder to better enable developers
  to both provide progress feedback to their users as well as enable them to
  better recover from exceptions (such as a dropped connection) occurring during
  the fetching of message summaries.
* Added support for the IMAP SORT=DISPLAY extension.
* Added a work-around for Cyrus IMAP 2.4.16 sending untagged SEARCH responses
  when untagged ESEARCH responses are expected.

### MailKit 1.0.12

* Fixed ImapFolder.GetMessage(), GetBodyPart() and GetStream() to throw an
  ImapCommandException rather than returning null if the server did not
  response with the message data.
* Added new, much more usable, Connect() methods to ImapClient, Pop3Client,
  and SmtpClient that take a hostname, port, and SecureSocketOptions.
* Added a workaround for smtp.strato.de's blatant disregard for standards.
  (issue #162)
* Fixed ImapFolder.Close() to require ReadWrite access if expunge is true.
* Fixed IMAP SORT queries to inject "RETURN" before the orderBy param.
  (issue #164)
* Implemented support for the IMAP ACL extension.

### MailKit 1.0.11

* Make sure that the IMAP stream supports timeouts before using them (fixes a
  regression introduced in 1.0.10).
* Added BodyParts and Attachments convenience properties to MessageSummary.
* Added TextBody and HtmlBody convenience properties to MessageSummary.
* Added ImapClient.IsAuthenticated, Pop3Client.IsAuthenticated and
  SmtpClient.IsAuthenticated properties.
* Changed the ImapClient.Inbox property to throw InvalidOperationException if
  you try to access it before authenticating instead of returning null.
* Added an ImapClient.IsIdle property to check if the ImapClient is currently
  in the IDLE state.

### MailKit 1.0.10

* Added support for the IMAP ID extension.

### MailKit 1.0.9

* Modified UniqueId to contain a Validity value. This allows ImapFolder.Append(),
  CopyTo(), and MoveTo() to provide the caller with a way to make sure that the
  UIDs are (still) valid in the destination folder at a future point in time.
* Modified ImapFolder.UidValidity to be a uint instead of a UniqueId which not
  only makes more sense but also simplifies comparison.
* Fixed GMail Label APIs to use the modified UTF-7 encoding logic meant for
  folder names as it appears that GMail wants label names to be encoded in this
  way. (issue #154)

### MailKit 1.0.8

* Fixed the SMTP BINARYMIME extension support to work properly. (issue #151)
* Fixed ImapFolder.Open() to not set the PermanentFlags to None if another
  folder was open (preventing SetFlags/AddFlags/RemoveFlags from functioning
  properly). (issue #153)

### MailKit 1.0.7

* Marked Pop3Client methods that take UIDs as [Obsolete]. It is suggested that
  the equivalent methods that take indexes be used instead and that UID-to-index
  mapping is done by the developer. This takes the burden off of the Pop3Client
  to maintain a mapping of UIDs to indexes that it cannot easily maintain.
* Fixed SmtpCommandException to only serialize the Mailbox property when it is
  non-null. (issue #148)
* Fixed IMAP support to accept a UIDVALIDITY value of 0 (even though it is
  technically illegal) to work around a bug in SmarterMail 13.0. (issue #150)
* Fixed ImapFolder.GetSubfolders() to filter out non-child folders from the list
  that it returns (once again, a work-around for a SmarterMail 13.0 bug).
  (issue #149)

### MailKit 1.0.6

* Fixed some issues revealed by source analysis.
* Migrated the iOS assemblies to Xamarin.iOS Unified API for 64-bit support.

Note: If you are not yet ready to port your iOS application to the Unified API,
      you will need to stick with the 1.0.5 release. The Classic MonoTouch API
      is no longer supported.

### MailKit 1.0.5

* Added Connect() overloads which takes a Socket argument (issue #128).
* Added support for SMTP Delivery Status Notifications (issue #136).
* Modified the ImapFolder logic such that if the IMAP server does not
  send a PERMANENTFLAGS resp-code when SELECTing the folder, then it
  will assume that all flags are permanent (issue #140).

### MailKit 1.0.4

* Modified the IMAP BODYSTRUCTURE parser to allow NIL tokens for
  Content-Type and Content-Disposition parameter values. (issue #124)
* Added ImapFolder.GetBodyPart() overrides to allow fetching body parts
  based on a part specifier string. (issue #130)

### MailKit 1.0.3

* Added a new ImapFolder.Fetch() overload that takes a HashSet<string>
  of header fields to fetch instead of a HashSet<HeaderId> for
  developers that need the ability to request custom headers not
  defined in the HeaderId enum.
* Added an SmtpClient.MessageSent event and an OnMessageSent() method
  that can be overridden.

### MailKit 1.0.2

* Modified ProtocolLogger to flush the stream at the end of each Log().
* Fixed IMAP SEARCH queries with empty string arguments.
* Fixed the IMAP FETCH parser to accept qstrings and literals for
  header field names.
* Improved documentation.

### MailKit 1.0.1

* Fixed Pop3Client.GetMessages (int startIndex, int count, ...) to use
  1-based sequence numbers.
* Fixed POP3 PIPELINING support to work as indtended (issue #114).
* Added a work-around for Office365.com IMAP to avoid
  ImapProtocolExceptions about unexpected '[' tokens when moving or
  copying messages between folders (issue #115).
* Disabled SSLv3 for security reasons (POODLE), opting instead to use
  TLS.
