# How to apply the row mouse hover effect in DataGrid(SfDataGrid)?

## About the sample
This example illustrates how to apply the row mouse hover effect in DataGrid(SfDataGrid)?

SfDataGrid allows you to change the color of the hovered row using the TableControl.MouseMove and QueryCellStyle events.

```C#
sfDataGrid1.TableControl.MouseMove += TableControl_MouseMove; 
sfDataGrid1.QueryCellStyle += sfDataGrid1_QueryCellStyle; 
sfDataGrid1.TableControl.MouseLeave += TableControl_MouseLeave; 
 
int hoveredRowIndex = -1;

void TableControl_MouseLeave(object sender, EventArgs e)
{
    //To remove the hovered row color while the mouse is leaves the SfDataGrid.
    sfDataGrid1.TableControl.Invalidate(sfDataGrid1.TableControl.GetRowRectangle(hoveredRowIndex, true));
    hoveredRowIndex = -1;
}

void sfDataGrid1_QueryCellStyle(object sender, Syncfusion.WinForms.DataGrid.Events.QueryCellStyleEventArgs e)
{
     if (e.RowIndex == hoveredRowIndex)
     {
          //Set the back color for the hovered row cells. 
          e.Style.BackColor = Color.Yellow;
     }
}

void TableControl_MouseMove(object sender, MouseEventArgs e)
{
     var rowColumnIndex = this.sfDataGrid1.TableControl.PointToCellRowColumnIndex(this.sfDataGrid1.TableControl.PointToClient(Cursor.Position));

     // Update the hovered row index. 
     if (hoveredRowIndex != rowColumnIndex.RowIndex)
     {         
         sfDataGrid1.TableControl.Invalidate(sfDataGrid1.TableControl.GetRowRectangle(hoveredRowIndex, true));
         hoveredRowIndex = rowColumnIndex.RowIndex;
         sfDataGrid1.TableControl.Invalidate(sfDataGrid1.TableControl.GetRowRectangle(hoveredRowIndex, true));
     }
}
 
```

## Requirements to run the demo
Visual Studio 2015 and above versions
