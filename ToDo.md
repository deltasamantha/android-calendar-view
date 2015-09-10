# To Do #

  1. start Calendar Activity with specified date by using uri parameter.
```
Uri day = Uri.parse("content://exina.android.calendar/view?year=2011&month=3&day=18");
startActivity(new Intent(Intent.ACTION_VIEW).setDataAndType(day, CalendarActivity.MIME_TYPE));
```