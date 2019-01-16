1. when using multi-gpu training the faster rcnn, the error will encountered:
"""
 ctx.input_sizes = tuple(map(lambda i: i.size(ctx.dim), inputs))
 RuntimeError: dimension specified as 0 but tensor has no dimensions
"""
yous should:
these lines just before returning the values in lib/model/faster_rcnn/faster_rcnn.py

"""
if self.training:
  rpn_loss_cls = torch.unsqueeze(rpn_loss_cls, 0)
  rpn_loss_bbox = torch.unsqueeze(rpn_loss_bbox, 0)
  RCNN_loss_cls = torch.unsqueeze(RCNN_loss_cls, 0)
  RCNN_loss_bbox = torch.unsqueeze(RCNN_loss_bbox, 0)
"""


2. when the loss is nan, it is probabley that the coordinate is smaller than 0, you should add a comment at the line 234 in lib/datasets/pascal_voc.py
