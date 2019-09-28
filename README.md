### boto3
---
https://github.com/boto/boto3

```py
// tests/integration/test_sqs.py
import boto3.session

from tests import unittest, unique_id

class TestSQSResource(unittest.TestCase):
  def setUp(self):
    self.session = boto3.session.Session(region_name='us-west-2')
    self.sqs = self.session.resource('sqs')
    self.queue_name = unique_id('boto3-test')
    
  def test_sqs(self):
    queue = self.sqs.create_queue(QueueName=self.queue_name)
    self.addCleanup(queue.delete)
    
    queue.send_message(MessageBody='test')
    
    messages = queue.receive_messages(WaitTimeSeconds=1)
    
    self.assertEqual(len(messages), 1)
    self.addCleanup(message[0].delete)
    
    self.assertEqual(queue.url, messages[0].queue_url)
    self.assertEqual('test', messages[0].body)
```

```
```

```
```


