---
subcategory: "EC2"
layout: "aws"
page_title: "AWS: aws_ebs_volume"
description: |-
  Provides an elastic block storage resource.
---

# Resource: aws_ebs_volume

Manages a single EBS volume.

## Example Usage

```hcl
resource "aws_ebs_volume" "example" {
  availability_zone = "us-west-2a"
  size              = 40

  tags = {
    Name = "HelloWorld"
  }
}
```

~> **NOTE**: One of `size` or `snapshot_id` is required when specifying an EBS volume

## Argument Reference

The following arguments are supported:

* `availability_zone` - (Required) The AZ where the EBS volume will exist.
* `encrypted` - (Optional) If true, the disk will be encrypted.
* `iops` - (Optional) The amount of IOPS to provision for the disk. Only valid for `type` of `io1` or `io2`.
* `multi_attach_enabled` - (Optional) Specifies whether to enable Amazon EBS Multi-Attach. Multi-Attach is supported exclusively on `io1` volumes.
* `size` - (Optional) The size of the drive in GiBs.
* `snapshot_id` (Optional) A snapshot to base the EBS volume off of.
* `outpost_arn` - (Optional) The Amazon Resource Name (ARN) of the Outpost.
* `type` - (Optional) The type of EBS volume. Can be "standard", "gp2", "io1", "io2", "sc1" or "st1" (Default: "gp2").
* `kms_key_id` - (Optional) The ARN for the KMS encryption key. When specifying `kms_key_id`, `encrypted` needs to be set to true.
* `tags` - (Optional) A map of tags to assign to the resource.

~> **NOTE**: When changing the `size`, `iops` or `type` of an instance, there are [considerations](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/considerations.html) to be aware of that Amazon have written about this.

## Attributes Reference

In addition to all arguments above, the following attributes are exported:

* `id` - The volume ID (e.g. vol-59fcb34e).
* `arn` - The volume ARN (e.g. arn:aws:ec2:us-east-1:0123456789012:volume/vol-59fcb34e).


## Import

EBS Volumes can be imported using the `id`, e.g.

```
$ terraform import aws_ebs_volume.id vol-049df61146c4d7901
```
