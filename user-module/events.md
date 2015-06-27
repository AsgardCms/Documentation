title: Events
subtitle: User Module
-------

The following events are triggered in the User Module:

- [UserHasRegistered](#user-has-registered)
- [UserHasBegunResetProcess](#user-has-begon-reset-process)
- [UserWasUpdated](#user-was-updated)
- [RoleWasUpdated](#role-was-updated)


### <a name="user-has-registered" class="anchor" href="#user-has-registered"></a> UserHasRegistered

Triggered when a user has registered. You have access to the complete User entity.

### <a name="user-has-begon-reset-process" class="anchor" href="#user-has-begon-reset-process"></a> UserHasBegunResetProcess

Triggered when a user has begun the reset password process. You have access to the complete User entity and the reset code that was generated.


### <a name="user-was-updated" class="anchor" href="#user-was-updated"></a> UserWasUpdated

Triggered when a user was updated in the administration. You have access to the complete User entity.


### <a name="role-was-updated" class="anchor" href="#role-was-updated"></a> RoleWasUpdated

Triggered when a role was updated in the administration. You have access to the complete Role entity.